# API Usage Example - Transition Vehicle Lifecycle Status

## Document Information
- Feature Name: Manage Vehicle Status and Availability
- Related TRD: [TRD - Manage Vehicle Status and Availability](../trd/trd-vehicle-status-availability.md)
- Author: copilot

## Table of Contents
- [Overview](#overview)
- [1. Submit a Triggering Event (System-to-System)](#1-submit-a-triggering-event-system-to-system)
- [2. Manually Override Status](#2-manually-override-status)
- [3. Get Current Status and Availability](#3-get-current-status-and-availability)
- [4. Get Status History](#4-get-status-history)
- [Error Responses](#error-responses)
- [AI usage disclaimer](#ai-usage-disclaimer)

## Overview
This document shows sample `curl` requests illustrating how a client would exercise the "Transition Vehicle Lifecycle Status" REST API contract defined in the [TRD - Manage Vehicle Status and Availability](../trd/trd-vehicle-status-availability.md). It is illustrative usage documentation only; it does not contain or imply any server-side implementation code.

All requests require an `Authorization` header carrying a signed JWT access token (see the TRD's Security Requirement section), shown below as `<JWT_ACCESS_TOKEN>`.

## 1. Submit a Triggering Event (System-to-System)
Used by trusted internal services (booking, handover/inspection, maintenance, compliance-monitor) to automatically transition a vehicle's lifecycle status when a triggering event occurs (e.g., `booking_confirmed`, `handover_completed`, `return_completed`, `maintenance_scheduled`, `damage_reported`).

- Method/URL: `POST /api/v1/vehicles/{vehicleId}/status-events`
- Required role: `system_service`

```bash
curl -X POST "https://api.example.com/api/v1/vehicles/9f8b6e2a-1c3d-4a5b-8e7f-1234567890ab/status-events" \
  -H "Authorization: <JWT_ACCESS_TOKEN>" \
  -H "Content-Type: application/json" \
  -d '{
        "eventType": "booking_confirmed",
        "effectiveAt": "2025-01-15T09:30:00Z",
        "reason": "Booking BR-10432 confirmed",
        "sourceSystem": "booking-service"
      }'
```

Sample response (`200 OK`):
```json
{
  "vehicleId": "9f8b6e2a-1c3d-4a5b-8e7f-1234567890ab",
  "status": "reserved",
  "statusSince": "2025-01-15T09:30:00Z"
}
```

## 2. Manually Override Status
Used by a `service_staff` or `operations_manager` to manually move a vehicle into a different status, with a mandatory reason (e.g., taking a vehicle out of service for an unscheduled inspection).

- Method/URL: `PATCH /api/v1/vehicles/{vehicleId}/status`
- Required role: `service_staff` or `operations_manager`

```bash
curl -X PATCH "https://api.example.com/api/v1/vehicles/9f8b6e2a-1c3d-4a5b-8e7f-1234567890ab/status" \
  -H "Authorization: <JWT_ACCESS_TOKEN>" \
  -H "Content-Type: application/json" \
  -d '{
        "newStatus": "maintenance",
        "reason": "Unscheduled brake inspection requested by staff"
      }'
```

Sample response (`200 OK`):
```json
{
  "vehicleId": "9f8b6e2a-1c3d-4a5b-8e7f-1234567890ab",
  "status": "maintenance",
  "statusSince": "2025-01-15T10:05:00Z"
}
```

## 3. Get Current Status and Availability
Used by any authenticated staff role to check a vehicle's current lifecycle status and whether it is available for booking.

- Method/URL: `GET /api/v1/vehicles/{vehicleId}/status`

```bash
curl -X GET "https://api.example.com/api/v1/vehicles/9f8b6e2a-1c3d-4a5b-8e7f-1234567890ab/status" \
  -H "Authorization: <JWT_ACCESS_TOKEN>"
```

Sample response (`200 OK`):
```json
{
  "vehicleId": "9f8b6e2a-1c3d-4a5b-8e7f-1234567890ab",
  "status": "maintenance",
  "statusSince": "2025-01-15T10:05:00Z",
  "available": false
}
```

## 4. Get Status History
Used to review the audit trail of every status transition for a vehicle, including the trigger and reason.

- Method/URL: `GET /api/v1/vehicles/{vehicleId}/status-history`

```bash
curl -X GET "https://api.example.com/api/v1/vehicles/9f8b6e2a-1c3d-4a5b-8e7f-1234567890ab/status-history?from=2025-01-01T00:00:00Z&to=2025-01-31T23:59:59Z" \
  -H "Authorization: <JWT_ACCESS_TOKEN>"
```

Sample response (`200 OK`):
```json
[
  {
    "previousStatus": "reserved",
    "newStatus": "maintenance",
    "triggerEvent": "manual_override",
    "reason": "Unscheduled brake inspection requested by staff",
    "effectiveAt": "2025-01-15T10:05:00Z"
  },
  {
    "previousStatus": "available",
    "newStatus": "reserved",
    "triggerEvent": "booking_confirmed",
    "reason": "Booking BR-10432 confirmed",
    "effectiveAt": "2025-01-15T09:30:00Z"
  }
]
```

## Error Responses
- `400 Bad Request` — invalid `status`/`newStatus`/`eventType`, or invalid/empty `reason` on manual override.
- `404 Not Found` — `vehicleId` does not reference an existing, non-deleted vehicle.
- `409 Conflict` — the requested transition is not allowed from the vehicle's current status.

Sample `409 Conflict` response when attempting an invalid transition (e.g., trying to move a `retired` vehicle to `available`):
```json
{
  "error": "conflict",
  "message": "Transition from 'retired' to 'available' is not permitted."
}
```

## AI usage disclaimer
*This document was generated with the assistance of artificial intelligence and should be reviewed by a human for accuracy and completeness.*

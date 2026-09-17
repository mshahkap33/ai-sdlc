# Draft Technical Standard - REST API

## Document Information
- Document Name: Technical Standard for REST API
- Author: copilot
- Date:
- Version: Draft

## Table of Contents
- [Purpose](#purpose)
- [Scope](#scope)
- [Resource Naming Conventions](#resource-naming-conventions)
- [URL Structure](#url-structure)
- [Versioning](#versioning)
- [HTTP Methods](#http-methods)
- [HTTP Status Codes](#http-status-codes)
- [Request Conventions](#request-conventions)
- [Response Conventions](#response-conventions)
- [Pagination](#pagination)
- [Filtering and Sorting](#filtering-and-sorting)
- [Error Handling](#error-handling)
- [Security](#security)
- [Idempotency](#idempotency)
- [Non-Functional Requirements](#non-functional-requirements)
- [AI Usage Disclaimer](#ai-usage-disclaimer)

## Purpose
This document proposes a company-wide technical standard for designing and implementing REST APIs across all business lines, including the new car rental business line. The goal is to ensure consistency, predictability, and interoperability between services and teams that design or consume REST APIs, regardless of the programming language or framework used.

This is a **draft** standard intended to be reviewed and adopted before being referenced by feature-specific Technical Requirement Documents (TRDs).

## Scope
- Applies to all new REST APIs built for internal or external consumption.
- Covers naming conventions, URL structure, versioning, HTTP method usage, status codes, request/response formats, pagination, filtering/sorting, error handling, security, and idempotency.
- Does not cover a specific feature's business logic; feature TRDs must reference this standard instead of redefining these conventions.
- Does not mandate a specific programming language, framework, or API gateway product.

## Resource Naming Conventions
- Resource names (URL path segments that identify a collection) must be **plural nouns**, written in **lower kebab-case** (e.g., `vehicle-categories`, not `VehicleCategory` or `vehicle_category`).
- Use nouns to represent resources; avoid verbs in the URL (actions are expressed through HTTP methods, e.g., use `POST /rentals` instead of `POST /create-rental`).
- Nested/sub-resources should reflect ownership hierarchy, e.g., `/rentals/{rentalId}/payments`.
- Query parameter names and JSON field names must use **lower snake_case** (e.g., `pickup_date`, `customer_id`).
- Path parameters must be named after the resource they identify with an `Id` suffix in camelCase, e.g., `{vehicleId}`, `{rentalId}`.
- Avoid abbreviations unless they are widely understood (e.g., `id`, `url`); prefer full, descriptive names.

## URL Structure
- Base URL format: `https://{host}/api/v{major-version}/{resource}`.
- Example: `https://api.example.com/api/v1/rentals/{rentalId}/payments`.
- Collection endpoint: `/api/v1/{resource}` (e.g., `/api/v1/rentals`).
- Single resource endpoint: `/api/v1/{resource}/{resourceId}` (e.g., `/api/v1/rentals/{rentalId}`).
- Actions that do not map cleanly to a CRUD operation on a resource (e.g., `cancel`, `extend`) should be modeled as a sub-resource or a state-changing verb appended after the resource identifier, e.g., `POST /api/v1/rentals/{rentalId}/cancel`. Use sparingly; prefer resource-oriented design first.

## Versioning
- APIs must be versioned using a **major version** number in the URL path (e.g., `/api/v1/...`).
- The major version must be incremented only for breaking changes (e.g., removing/renaming a field, changing a field's data type, changing authentication requirements).
- Non-breaking, additive changes (e.g., adding a new optional field, adding a new endpoint) do not require a version increase.
- Each major version must be supported for a defined deprecation window (to be agreed per project) before being retired, and deprecation must be communicated in advance (e.g., via a `Deprecation` and `Sunset` response header).
- Minor/patch level changes are not reflected in the URL; they are tracked through release notes/changelogs.

## HTTP Methods
| Method | Usage | Idempotent |
|---|---|---|
| `GET` | Retrieve a single resource or a collection. Must not have side effects. | Yes |
| `POST` | Create a new resource, or trigger an action that is not a simple CRUD operation. | No |
| `PUT` | Replace a resource entirely with the provided representation. | Yes |
| `PATCH` | Partially update a resource with only the provided fields. | No (unless explicitly designed to be) |
| `DELETE` | Remove a resource. | Yes |

- Prefer `PATCH` over `PUT` when only a subset of fields is expected to change, to reduce accidental overwrites.

## HTTP Status Codes
- `200 OK` — Successful `GET`, `PUT`, `PATCH`, or `DELETE` that returns a body.
- `201 Created` — Successful `POST` that creates a resource; must include a `Location` header pointing to the new resource.
- `202 Accepted` — Request accepted for asynchronous processing.
- `204 No Content` — Successful request with no response body (e.g., `DELETE`).
- `400 Bad Request` — Malformed request or failed validation.
- `401 Unauthorized` — Missing or invalid authentication credentials.
- `403 Forbidden` — Authenticated but not authorized to perform the action.
- `404 Not Found` — Resource does not exist.
- `409 Conflict` — Request conflicts with the current state of the resource (e.g., duplicate booking, optimistic locking conflict).
- `422 Unprocessable Entity` — Well-formed request that fails business validation rules.
- `429 Too Many Requests` — Rate limit exceeded.
- `500 Internal Server Error` — Unexpected server-side failure.
- `503 Service Unavailable` — Service temporarily unavailable (e.g., maintenance, downstream dependency failure).

## Request Conventions
- Request and response bodies must use `application/json` content type, encoded in UTF-8.
- All timestamps must be in ISO 8601 format with a timezone offset (e.g., `2024-05-01T10:00:00Z`).
- All monetary amounts must be represented as a string or decimal type (never a floating-point binary type) with an explicit currency code field (e.g., `amount: "150.00"`, `currency: "USD"`).
- Required and optional fields must be explicitly documented for every endpoint in the feature TRD.
- Requests must include a `Content-Type: application/json` header; the server must reject unsupported content types with `415 Unsupported Media Type`.

## Response Conventions
- A single resource response returns a flat JSON object representing that resource.
- A collection response must wrap the list of items in a `data` field, alongside pagination metadata, e.g.:
```
{
  "data": [ { ... }, { ... } ],
  "pagination": { "page": 1, "page_size": 20, "total_items": 42 }
}
```
- Field names in responses must match the snake_case convention described above.
- Every resource representation should include `created_at` and `updated_at` timestamps where applicable.

## Pagination
- Collection endpoints must support pagination using `page` (1-indexed) and `page_size` query parameters.
- Default and maximum `page_size` values must be explicitly defined per endpoint to prevent excessive load.
- Pagination metadata (`page`, `page_size`, `total_items`, `total_pages`) must be returned alongside the `data` array, as shown in [Response Conventions](#response-conventions).
- Cursor-based pagination may be used instead of offset-based pagination for high-volume or frequently changing datasets; this choice must be documented in the feature TRD.

## Filtering and Sorting
- Filtering is done via query parameters matching the field name (e.g., `?status=active`).
- Sorting is done via a `sort` query parameter, with an optional `-` prefix for descending order (e.g., `?sort=-created_at`).
- Multiple sort fields are comma-separated (e.g., `?sort=-created_at,make`).
- Unsupported filter or sort fields must result in a `400 Bad Request`.

## Error Handling
- Error responses must use a consistent JSON structure across all APIs:
```
{
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Human-readable summary of the error",
    "details": [
      { "field": "pickup_date", "message": "must be a future date" }
    ]
  }
}
```
- `code` must be a stable, machine-readable identifier (upper snake case) that does not change across releases, so clients can programmatically branch on it.
- `message` is a human-readable description intended for logs/developers, not for direct end-user display.
- `details` is optional and used for field-level validation errors.

## Security
- All APIs must be served over HTTPS/TLS; plain HTTP is not allowed.
- Authentication must use a bearer token scheme (e.g., JWT) passed via the `Authorization` HTTP header using the `Bearer` scheme, unless a feature TRD explicitly justifies an alternative.
- Authorization checks must be enforced on every endpoint; a valid token alone must not be sufficient to access another user's resources.
- Sensitive fields (e.g., payment details, personal identification numbers) must never be logged and must be masked in responses when not strictly required.
- Rate limiting must be applied per client/API key to protect against abuse; exceeding the limit returns `429 Too Many Requests` with a `Retry-After` header.
- Detailed authentication/authorization mechanisms (e.g., specific JWT algorithm, token payload, token issuer) must be defined per feature TRD's Security Requirement section, following this standard as the baseline.

## Idempotency
- `PUT` and `DELETE` requests must be idempotent: repeating the same request must produce the same end state without unintended side effects.
- For `POST` requests that create resources and must be safely retried (e.g., payment creation), clients must be able to supply an `Idempotency-Key` header; the server must return the original result for duplicate keys instead of creating a duplicate resource.

## Non-Functional Requirements
Leave blank

## AI Usage Disclaimer
This document was generated with the assistance of artificial intelligence and should be reviewed by a human for accuracy and completeness.

# Test Scenario - Manage Vehicle Status and Availability

## Document Information
- Author: copilot
- Date:
- Version:

## Table of Contents
- [Test Scenario](#test-scenario)
- [Test Case 1](#test-case-1)
- [Test Case 2](#test-case-2)
- [Test Case 3](#test-case-3)

## Test Scenario
- **Feature to test:** Validate the [Manage Vehicle Status and Availability](../../prd/prd-car-management.md#manage-vehicle-status-and-availability) capability, which tracks vehicle status and automatically transitions it based on triggering events, compliance document expiry, and recalls.
- **Preconditions:**
  - The Car Management application is running.
  - A vehicle exists with status "available".

## Test Case 1
- **Description:** Automatic status transition to "reserved" when a booking is confirmed.
- **Steps:**
  1. Create a booking for the vehicle.
  2. Confirm the booking.
  3. View the vehicle's current status.
- **Expected result:** The vehicle status changes to "reserved" and the vehicle cannot be booked by another customer for the overlapping period.

## Test Case 2
- **Description:** Automatic status transition to unavailable when a compliance document expires.
- **Steps:**
  1. Set the vehicle's registration (or insurance/inspection) expiry date to a date in the past.
  2. Allow the expiry condition to be detected by the system.
  3. View the vehicle's current status.
- **Expected result:** The vehicle is automatically marked unavailable and cannot be booked until the expired document is resolved/renewed.

## Test Case 3
- **Description:** Automatic status transition to unavailable when a recall is opened, and restoration once resolved.
- **Steps:**
  1. Log an open recall against the vehicle.
  2. View the vehicle's current status.
  3. Resolve/close the recall.
  4. View the vehicle's current status again.
- **Expected result:** The vehicle is marked unavailable while the recall is open, and automatically returns to its prior available status once the recall is resolved.

## AI Usage Disclaimer
*This document was generated with the assistance of artificial intelligence and should be reviewed by a human for accuracy and completeness.*

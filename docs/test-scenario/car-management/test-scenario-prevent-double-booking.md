# Test Scenario - Prevent Double-Booking

## Document Information
- Author: copilot
- Date:
- Version:

## Table of Contents
- [Test Scenario](#test-scenario)
- [Test Case 1](#test-case-1)
- [Test Case 2](#test-case-2)

## Test Scenario
- **Feature to test:** Validate the [Prevent Double-Booking](../../prd/prd-car-management.md#prevent-double-booking) capability, which validates vehicle availability against existing reservations and current status before confirming any new booking or vehicle assignment.
- **Preconditions:**
  - The Car Management application is running.
  - A vehicle has a confirmed reservation for a specific date/time period.

## Test Case 1
- **Description:** Rejecting a new booking that overlaps an existing confirmed reservation for the same vehicle.
- **Steps:**
  1. Identify a vehicle with an existing confirmed reservation for a given time period.
  2. Attempt to create a new booking for the same vehicle with a time period that overlaps the existing reservation.
- **Expected result:** The system rejects or blocks the conflicting booking and does not create a second reservation for the overlapping period.

## Test Case 2
- **Description:** Allowing a new booking for the same vehicle when the requested period does not overlap an existing reservation.
- **Steps:**
  1. Identify a vehicle with an existing confirmed reservation for a given time period.
  2. Create a new booking for the same vehicle with a time period that does not overlap the existing reservation.
- **Expected result:** The new booking is accepted and confirmed successfully, since there is no time-period conflict.

## AI Usage Disclaimer
*This document was generated with the assistance of artificial intelligence and should be reviewed by a human for accuracy and completeness.*

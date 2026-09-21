# Test Scenario - Confirm Handover and Capture Condition

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
- **Feature to test:** Validate the [Confirm Handover and Capture Condition](../../prd/prd-car-management.md#confirm-handover-and-capture-condition) capability, which supports a digital handover process capturing signature, ID check, photos, condition checklist, fuel/mileage, geolocation, and timestamp, and handles exception scenarios.
- **Preconditions:**
  - The Car Management application is running.
  - A scheduled pickup/delivery/handover event exists for a confirmed booking.

## Test Case 1
- **Description:** Completing a digital handover checklist successfully.
- **Steps:**
  1. Open the scheduled handover event.
  2. Capture the customer's signature and complete the ID check.
  3. Capture required photos and complete the condition checklist.
  4. Enter the current fuel level and mileage.
  5. Submit the handover.
- **Expected result:** The handover record is saved with all captured evidence (signature, ID check, photos, condition, fuel/mileage, geolocation, timestamp), and the vehicle status is updated accordingly (e.g., to "rented").

## Test Case 2
- **Description:** Flagging a handover exception when the customer is unavailable.
- **Steps:**
  1. Open the scheduled handover event.
  2. Attempt to contact the customer at the scheduled time and location.
  3. Flag the event as "customer unavailable".
- **Expected result:** The system records the exception and prompts staff for next steps (e.g., reschedule the handover).

## Test Case 3
- **Description:** Flagging a handover exception when the delivery address is incorrect.
- **Steps:**
  1. Open the scheduled handover event.
  2. Arrive at the specified address and determine it is incorrect.
  3. Flag the event as "incorrect address".
- **Expected result:** The system records the exception and prompts staff for next steps (e.g., obtain corrected address and reschedule).

## AI Usage Disclaimer
*This document was generated with the assistance of artificial intelligence and should be reviewed by a human for accuracy and completeness.*

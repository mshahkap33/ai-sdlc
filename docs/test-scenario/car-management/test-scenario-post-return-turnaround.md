# Test Scenario - Manage Post-Return Turnaround

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
- **Feature to test:** Validate the [Manage Post-Return Turnaround](../../prd/prd-car-management.md#manage-post-return-turnaround) capability, which generates post-return tasks (cleaning, refueling, repair), tracks turnaround time, and tracks lost keys/accessories/documents.
- **Preconditions:**
  - The Car Management application is running.
  - A vehicle has just completed its return inspection.

## Test Case 1
- **Description:** Automatic generation of post-return tasks after a return inspection is completed.
- **Steps:**
  1. Complete the return inspection for a vehicle.
  2. View the vehicle's post-return task list.
- **Expected result:** Applicable tasks (e.g., cleaning, refueling, repair) are automatically created based on the return inspection findings.

## Test Case 2
- **Description:** Vehicle status returns to "available" once all post-return tasks are completed and final checks pass.
- **Steps:**
  1. Mark all generated post-return tasks (cleaning, refueling, repair) as completed.
  2. Perform the final check on the vehicle.
  3. View the vehicle's current status.
- **Expected result:** The vehicle's status is updated to "available" once all tasks are completed and final checks pass.

## Test Case 3
- **Description:** Recording lost keys, accessories, or documents identified during the return process.
- **Steps:**
  1. Open the return record for a vehicle.
  2. Flag a lost key, accessory, or document as missing.
  3. Save the return record.
- **Expected result:** The missing item is recorded against the return record and is visible for follow-up/tracking.

## AI Usage Disclaimer
*This document was generated with the assistance of artificial intelligence and should be reviewed by a human for accuracy and completeness.*

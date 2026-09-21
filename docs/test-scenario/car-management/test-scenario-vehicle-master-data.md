# Test Scenario - Maintain Vehicle Master Data

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
- **Feature to test:** Validate the [Maintain Vehicle Master Data](../../prd/prd-car-management.md#maintain-vehicle-master-data) capability, which allows Service staff to create and update core vehicle data (VIN, plate, make/model, mileage, fuel level, location, condition) and to group vehicles by category/class for booking purposes.
- **Preconditions:**
  - The Car Management application is running and accessible to a logged-in Service staff user.
  - At least one vehicle category/class (e.g., "Economy", "SUV") already exists in the system.

## Test Case 1
- **Description:** Creating a new vehicle record with all required identity and condition data.
- **Steps:**
  1. Navigate to the "Add Vehicle" screen.
  2. Enter a unique VIN, plate number, make/model, and year.
  3. Enter mileage, fuel level, current location, and condition notes.
  4. Select an existing vehicle category/class for the vehicle.
  5. Save the vehicle record.
- **Expected result:** The vehicle record is created successfully, is visible in the fleet list, and is shown as belonging to the selected category/class.

## Test Case 2
- **Description:** Updating mileage, fuel level, and location on an existing vehicle record.
- **Steps:**
  1. Open an existing vehicle record.
  2. Update the mileage value, fuel level, and current location.
  3. Save the changes.
- **Expected result:** The vehicle record immediately reflects the updated mileage, fuel level, and location values.

## Test Case 3
- **Description:** Preventing creation of a vehicle with a duplicate VIN or plate.
- **Steps:**
  1. Navigate to the "Add Vehicle" screen.
  2. Enter a VIN or plate number that already exists on another vehicle record.
  3. Complete the remaining required fields.
  4. Attempt to save the vehicle record.
- **Expected result:** The system rejects the save with a validation error indicating the VIN/plate is already in use, and no duplicate vehicle record is created.

## AI Usage Disclaimer
*This document was generated with the assistance of artificial intelligence and should be reviewed by a human for accuracy and completeness.*

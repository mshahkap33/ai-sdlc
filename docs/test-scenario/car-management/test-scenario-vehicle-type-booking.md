# Test Scenario - Vehicle-Level and Category-Level Booking

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
- **Feature to test:** Validate the [Support Vehicle-Level and Category-Level Booking](../../prd/prd-car-management.md#support-vehicle-level-and-category-level-booking) capability, which allows a customer to reserve either a specific vehicle or a vehicle category, depending on the configured booking policy.
- **Preconditions:**
  - The Car Management application is running.
  - At least one vehicle category exists with two or more available vehicles.
  - A booking policy is configured for the vehicle category.

## Test Case 1
- **Description:** Booking an exact vehicle when the category's booking policy allows vehicle-level selection.
- **Steps:**
  1. Set the booking policy for a vehicle category to allow exact-vehicle selection.
  2. Create a booking that selects a specific VIN/plate within that category.
  3. Confirm the booking.
- **Expected result:** The exact vehicle selected is held for the reservation and is not available for assignment to any other booking.

## Test Case 2
- **Description:** Booking a category only, when the booking policy allows only category-level selection.
- **Steps:**
  1. Set the booking policy for a vehicle category to allow only category-level selection.
  2. Create a booking that selects the category without specifying an exact vehicle.
  3. Confirm the booking.
- **Expected result:** The booking is accepted against the category, and any available vehicle within that category may be assigned to it at fulfillment time.

## Test Case 3
- **Description:** Rejecting an exact-vehicle booking request when the policy only allows category-level selection.
- **Steps:**
  1. Set the booking policy for a vehicle category to allow only category-level selection.
  2. Attempt to create a booking that selects a specific VIN/plate within that category.
- **Expected result:** The system rejects the exact-vehicle booking request and indicates that only category-level booking is permitted for that category.

## AI Usage Disclaimer
*This document was generated with the assistance of artificial intelligence and should be reviewed by a human for accuracy and completeness.*

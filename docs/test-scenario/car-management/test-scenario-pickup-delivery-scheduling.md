# Test Scenario - Schedule Pickup and Delivery

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
- **Feature to test:** Validate the [Schedule Pickup and Delivery](../../prd/prd-car-management.md#schedule-pickup-and-delivery) capability, which allows staff to schedule pickup/delivery events across multiple location models, capturing address, contact, time window, vehicle requirements, and applicable fees.
- **Preconditions:**
  - The Car Management application is running.
  - A confirmed rental booking exists that requires delivery.

## Test Case 1
- **Description:** Scheduling a delivery to a customer address with a calculated delivery fee.
- **Steps:**
  1. Open the confirmed rental booking that requires delivery.
  2. Select "Customer Address" as the delivery model and enter the delivery address, contact information, and desired time window.
  3. Save the delivery schedule.
- **Expected result:** The system records the location, contact, time window, and vehicle requirements, and calculates and displays the applicable delivery fee based on distance/location/vehicle type/time.

## Test Case 2
- **Description:** Viewing the assigned driver/route for a scheduled pickup/delivery.
- **Steps:**
  1. Schedule a pickup or delivery for a confirmed booking.
  2. Assign a driver/route to the scheduled event.
  3. Open the pickup/delivery view as a Delivery/Pickup staff member.
- **Expected result:** The assigned driver/route is visible to the delivery/pickup staff for the scheduled event.

## Test Case 3
- **Description:** Scheduling pickup/delivery at a non-branch location model (e.g., airport, hotel, partner location).
- **Steps:**
  1. Open a confirmed rental booking requiring pickup/delivery.
  2. Select a location model other than the branch/dealership (e.g., airport, hotel, or partner location).
  3. Enter the required address, contact information, time window, and vehicle requirements.
  4. Save the schedule.
- **Expected result:** The pickup/delivery event is recorded correctly for the selected non-branch location model with all required details captured.

## AI Usage Disclaimer
*This document was generated with the assistance of artificial intelligence and should be reviewed by a human for accuracy and completeness.*

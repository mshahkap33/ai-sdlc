# Test Scenario - Schedule and Track Maintenance

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
- **Feature to test:** Validate the [Schedule and Track Maintenance](../../prd/prd-car-management.md#schedule-and-track-maintenance) capability, which triggers and tracks maintenance based on date, mileage, telematics, or manufacturer schedule, prioritizes urgent repairs/recalls/safety defects, and generates alerts for overdue service, expiring documents, and recalls.
- **Preconditions:**
  - The Car Management application is running.
  - A vehicle has a configured maintenance schedule (date and/or mileage based).

## Test Case 1
- **Description:** Automatic generation of a maintenance alert/work order when a mileage threshold is reached.
- **Steps:**
  1. Update the vehicle's mileage to a value that meets or exceeds its configured mileage-based maintenance threshold.
  2. Allow the threshold condition to be evaluated by the system.
  3. View the vehicle's maintenance alerts/work orders.
- **Expected result:** A maintenance alert/work order is generated for the vehicle.

## Test Case 2
- **Description:** Prioritizing a logged recall/safety defect over routine maintenance.
- **Steps:**
  1. Log a recall or safety defect against a vehicle that also has a routine maintenance item pending.
  2. View the vehicle's maintenance/work order queue.
- **Expected result:** The vehicle is flagged for urgent attention, and the recall/safety defect work order is prioritized ahead of the routine maintenance item.

## Test Case 3
- **Description:** Generating an alert for an overdue service or an expiring compliance document.
- **Steps:**
  1. Set a vehicle's scheduled service date to a date in the past without the service being marked complete, or set a compliance document (registration/insurance) to expire within the alerting window.
  2. Allow the system to evaluate overdue/expiring conditions.
  3. View the maintenance/compliance alerts list.
- **Expected result:** An alert is generated indicating the vehicle has overdue service or an expiring document/recall requiring attention.

## AI Usage Disclaimer
*This document was generated with the assistance of artificial intelligence and should be reviewed by a human for accuracy and completeness.*

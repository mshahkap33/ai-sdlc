# Test Scenario - View Operational Dashboards and Alerts

## Document Information
- Author: copilot
- Date:
- Version:

## Table of Contents
- [Test Scenario](#test-scenario)
- [Test Case 1](#test-case-1)
- [Test Case 2](#test-case-2)

## Test Scenario
- **Feature to test:** Validate the [View Operational Dashboards and Alerts](../../prd/prd-car-management.md#view-operational-dashboards-and-alerts) capability, which provides a daily operational dashboard summarizing pickups, returns, late vehicles, maintenance backlog, and utilization, and alerts relevant staff when a vehicle is overdue, damaged, or mislocated.
- **Preconditions:**
  - The Car Management application is running.
  - An Operations manager is logged in.
  - The fleet has a mix of vehicles with pickups, returns, and maintenance activity scheduled or in progress for the current day.

## Test Case 1
- **Description:** Loading the daily operational dashboard with current fleet activity.
- **Steps:**
  1. Log in as an Operations manager.
  2. Open the daily operational dashboard.
- **Expected result:** The dashboard displays current pickups, returns, late vehicles, maintenance backlog, and utilization metrics for the fleet.

## Test Case 2
- **Description:** Alerting staff when a vehicle becomes overdue, damaged, or mislocated.
- **Steps:**
  1. Cause a rented vehicle's scheduled return time to pass without the return being recorded (overdue), or report a vehicle as damaged, or record a vehicle at a location different from its expected location (mislocated).
  2. Allow the system to evaluate the condition.
  3. Check the alerts available to the appropriate staff.
- **Expected result:** The appropriate staff are alerted about the overdue, damaged, or mislocated vehicle condition.

## AI Usage Disclaimer
*This document was generated with the assistance of artificial intelligence and should be reviewed by a human for accuracy and completeness.*

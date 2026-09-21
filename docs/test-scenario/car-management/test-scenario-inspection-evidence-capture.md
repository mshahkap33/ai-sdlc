# Test Scenario - Perform Inspections and Capture Evidence

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
- **Feature to test:** Validate the [Perform Inspections and Capture Evidence](../../prd/prd-car-management.md#perform-inspections-and-capture-evidence) capability, which allows Service staff to record inspections before pickup, at handover, and on return, capturing photos, video, checklist, signature, geolocation, and timestamp, and to record and classify damage.
- **Preconditions:**
  - The Car Management application is running.
  - A vehicle has a completed prior inspection record on file (e.g., from the handover inspection).

## Test Case 1
- **Description:** Performing a return inspection and flagging new damage found.
- **Steps:**
  1. Open the return inspection for the vehicle being returned.
  2. Capture photos, video, checklist responses, signature, geolocation, and timestamp.
  3. Complete the inspection.
- **Expected result:** The system captures all required evidence for the return inspection and flags any new damage found compared to the prior (handover) inspection.

## Test Case 2
- **Description:** Classifying identified damage and linking it to a billing action.
- **Steps:**
  1. Open an inspection where damage was identified.
  2. Classify the damage (e.g., type and severity).
  3. Confirm the classification.
- **Expected result:** The damage record is saved with its classification and is linked to a billing action where applicable.

## Test Case 3
- **Description:** Performing a pre-pickup inspection before the vehicle is dispatched.
- **Steps:**
  1. Open the pre-pickup inspection for a vehicle scheduled for dispatch.
  2. Capture photos, checklist responses, signature, geolocation, and timestamp.
  3. Complete the inspection.
- **Expected result:** The pre-pickup inspection record is saved and available as the baseline for comparison during the subsequent handover inspection.

## AI Usage Disclaimer
*This document was generated with the assistance of artificial intelligence and should be reviewed by a human for accuracy and completeness.*

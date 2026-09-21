# Test Scenario - Customer Segmentation and Targeting

## Document Information
- Author: copilot
- Date:
- Version:

## Table of Contents
- [Test Scenario](#test-scenario)
- [Test Case 1](#test-case-1)
- [Test Case 2](#test-case-2)
- [Test Case 3](#test-case-3)
- [Test Case 4](#test-case-4)

## Test Scenario

**Feature to test:** Validate that Marketing can define reusable customer segments and use customer data (location, rental history, car-sales history, preferences) to personalize offers and campaign targeting, as described in the [Marketing PRD](../../prd/prd-marketing.md#customer-segmentation-and-targeting).

**Preconditions:**
- Marketing application/system is running and accessible to a marketing manager.
- Predefined segment types exist: individual consumers, corporate clients, travel agencies, insurers, existing car-sales customers.
- Test customer records exist with rental history, car-sales history, location, and stated preferences.

## Test Case 1

**Description:** Selecting predefined segment types when creating a campaign.

**Steps:**
1. Log in as a marketing manager.
2. Start creating a new campaign.
3. Open the target segment selection step.
4. Review the list of available segment types.

**Expected result:** The marketing manager can choose from the predefined segment types: individual consumers, corporate clients, travel agencies, insurers, and existing car-sales customers.

## Test Case 2

**Description:** Reusing an existing segment definition across multiple campaigns.

**Steps:**
1. Create a segment definition (e.g., "Corporate Clients - Region A").
2. Create Campaign A and assign the segment to it.
3. Create Campaign B and assign the same segment to it.
4. Verify both campaigns reference the same segment definition.

**Expected result:** The segment definition is reused in both campaigns without needing to be recreated.

## Test Case 3

**Description:** Targeting customers using rental history as a rule.

**Steps:**
1. Create a campaign targeting rule referencing prior rental history (e.g., "customers with at least 1 completed rental").
2. Apply the rule to a set of test customers, some with rental history and some without.
3. Run the targeting evaluation.

**Expected result:** Only customers matching the rental history condition are included in the resulting audience.

## Test Case 4

**Description:** Targeting customers using linked car-sales history as a rule.

**Steps:**
1. Create a campaign targeting rule referencing car-sales history (e.g., "customers with a prior car purchase").
2. Apply the rule to a set of test customers, some with linked car-sales history and some without.
3. Run the targeting evaluation.

**Expected result:** Car-sales history data is available for targeting, and only customers matching the rule are included in the resulting audience.

## AI Usage Disclaimer
*This document was generated with the assistance of artificial intelligence and should be reviewed by a human for accuracy and completeness.*

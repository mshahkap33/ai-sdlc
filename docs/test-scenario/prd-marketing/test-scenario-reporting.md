# Test Scenario - Reporting

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

**Feature to test:** Validate marketing performance reporting (conversion rate, campaign ROI, promo usage, CAC, repeat-rental rate, CLV), linking rental activity to existing car-sales customer records, and timely availability of customer feedback data to marketing, as described in the [Marketing PRD](../../prd/prd-marketing.md#reporting).

**Preconditions:**
- Marketing application/system is running and accessible to a marketing manager.
- Campaign, booking, and promotion data exists in the system.
- Both rental-only and matched rental/car-sales customer records exist.
- Post-rental feedback and review data can be submitted.

## Test Case 1

**Description:** Generating a marketing performance report with all required metrics.

**Steps:**
1. Log in as a marketing manager.
2. Navigate to the reporting section.
3. Request a marketing performance report.

**Expected result:** The report includes conversion rate, campaign ROI, promo usage, customer acquisition cost (CAC), repeat-rental rate, and customer lifetime value (CLV).

## Test Case 2

**Description:** Filtering a report by a specific campaign or promotion.

**Steps:**
1. Generate a marketing performance report.
2. Apply a filter for a specific campaign or promotion.

**Expected result:** The report reflects data only for the selected campaign or promotion.

## Test Case 3

**Description:** Unified profile view for a rental customer matched to an existing car-sales customer.

**Steps:**
1. Identify a rental customer record that matches an existing car-sales customer.
2. View the customer's profile.
3. Repeat for a rental customer with no matching car-sales record.

**Expected result:** For the matched customer, both rental and car-sales activity are visible together on the profile. For the unmatched customer, only rental activity is shown until a match is established.

## Test Case 4

**Description:** Post-rental feedback becomes visible to marketing reporting within a defined timeframe.

**Steps:**
1. Have a test customer submit post-rental feedback, including a review score.
2. Wait for the defined processing timeframe.
3. View marketing reporting for that customer/rental.

**Expected result:** The feedback record, including the review score, is visible in marketing reporting within the defined timeframe.

## AI Usage Disclaimer
*This document was generated with the assistance of artificial intelligence and should be reviewed by a human for accuracy and completeness.*

# Test Scenario - Promotions

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
- [Test Case 5](#test-case-5)
- [Test Case 6](#test-case-6)
- [Test Case 7](#test-case-7)

## Test Scenario

**Feature to test:** Validate that Marketing can create and configure promotions (promo codes, discounts, bundles, referral programs, loyalty rewards), define eligibility rules, resolve stacking/priority when multiple promotions apply, and scope campaigns/promotions to inventory, location, or low-demand periods, as described in the [Marketing PRD](../../prd/prd-marketing.md#promotions).

**Preconditions:**
- Marketing application/system is running and accessible to a marketing manager.
- Rental booking, pricing, and inventory data are available.
- Test bookings can be created with configurable dates, vehicle category, location, and rental length.

## Test Case 1

**Description:** Creating each supported promotion type.

**Steps:**
1. Log in as a marketing manager.
2. Create a new promotion and select type "promo code"; configure and save.
3. Repeat for "discount" (percentage or fixed), "bundle", "referral program", and "loyalty reward".

**Expected result:** Each promotion type can be configured and saved successfully as a promo code, discount, bundle, referral program, or loyalty reward.

## Test Case 2

**Description:** Activating a promotion makes it available according to its configured rules.

**Steps:**
1. Create a promotion with defined rules.
2. Activate the promotion.
3. Attempt to apply it to a booking that satisfies the rules.

**Expected result:** Once activated, the promotion becomes available and can be applied to bookings that meet its configured rules.

## Test Case 3

**Description:** Promotion applies when a booking meets all configured eligibility rules.

**Steps:**
1. Create a promotion with eligibility rules: eligible dates, vehicle category, location, and minimum rental length.
2. Create a booking that satisfies all of the configured rules.
3. Attempt to apply the promotion to the booking.

**Expected result:** The promotion is applicable and applies to the booking.

## Test Case 4

**Description:** Promotion does not apply when a booking fails to meet one or more eligibility rules.

**Steps:**
1. Create a promotion with eligibility rules: eligible dates, vehicle category, location, and minimum rental length.
2. Create a booking that violates at least one rule (e.g., rental length shorter than the minimum).
3. Attempt to apply the promotion to the booking.

**Expected result:** The promotion is not applied to the booking.

## Test Case 5

**Description:** Selecting a single applicable promotion when multiple non-stackable promotions are eligible.

**Steps:**
1. Configure two or more promotions, none marked as stackable, that are all eligible for the same reservation.
2. Price the reservation.

**Expected result:** Only one promotion is applied to the reservation, chosen based on the defined selection method (e.g., best discount for the customer or priority order).

## Test Case 6

**Description:** Applying multiple promotions when explicitly configured as stackable.

**Steps:**
1. Configure two promotions and mark them as stackable with each other.
2. Ensure both promotions are eligible for the same reservation.
3. Price the reservation.

**Expected result:** Both stackable promotions are applied to the reservation.

## Test Case 7

**Description:** Scoping a campaign/promotion to specific inventory, location, or low-demand period.

**Steps:**
1. Scope a campaign or promotion to specific vehicle inventory and a specific rental location.
2. Attempt a booking outside the scoped inventory/location.
3. Scope another campaign or promotion to a low-demand date range.
4. Attempt a booking within that date range.

**Expected result:** The booking outside the scoped inventory/location does not receive the campaign/promotion; the booking within the low-demand date range is eligible for the campaign/promotion.

## AI Usage Disclaimer
*This document was generated with the assistance of artificial intelligence and should be reviewed by a human for accuracy and completeness.*

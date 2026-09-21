# Test Scenario - Customer Communications

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
- [Test Case 8](#test-case-8)

## Test Scenario

**Feature to test:** Validate automated lifecycle communications, marketing vs. operations/legal content ownership, multi-language support, consent capture, and campaign attribution tracking, as described in the [Marketing PRD](../../prd/prd-marketing.md#customer-communications).

**Preconditions:**
- Marketing application/system is running and accessible to a marketing manager.
- Test customer records exist with configurable consent status and preferred language.
- A rental booking lifecycle (booking, pre-rental, completion) can be simulated.

## Test Case 1

**Description:** Automated booking confirmation is sent when a rental is booked.

**Steps:**
1. Create and confirm a rental booking for a test customer.

**Expected result:** An automated confirmation message is sent to the customer.

## Test Case 2

**Description:** Automated receipt and survey are sent after rental completion.

**Steps:**
1. Complete a rental for a test customer.
2. Allow the post-rental process to run.

**Expected result:** A receipt and a post-rental survey are sent automatically to the customer.

## Test Case 3

**Description:** Marketing user cannot edit operations/legal-controlled content.

**Steps:**
1. Mark a communication template as operations/legal-controlled (e.g., contractual terms).
2. Log in as a marketing user (without elevated permissions).
3. Attempt to edit the template.

**Expected result:** The system prevents the edit, or restricts it so only authorized roles can make the change.

## Test Case 4

**Description:** Marketing user can edit marketing-controlled content.

**Steps:**
1. Mark a communication template as marketing-controlled (e.g., promotional messaging).
2. Log in as a marketing user.
3. Edit the template and save.

**Expected result:** The change is allowed and saved successfully.

## Test Case 5

**Description:** Communication is delivered in the customer's preferred language when available.

**Steps:**
1. Set a customer's preferred language (e.g., Spanish) on file, with a translation available.
2. Trigger an automated communication for that customer.

**Expected result:** The communication is delivered in the customer's preferred language.

## Test Case 6

**Description:** Default language is used when no preferred language is on file.

**Steps:**
1. Ensure a customer has no preferred language on file.
2. Trigger an automated communication for that customer.

**Expected result:** The communication is sent using the system's default language.

## Test Case 7

**Description:** Marketing messages are blocked without consent, and sent with consent retained.

**Steps:**
1. For Customer A, ensure no marketing consent has been recorded; trigger a marketing message.
2. For Customer B, record valid marketing consent; trigger a marketing message.

**Expected result:** The message to Customer A is not sent. The message to Customer B is sent, and the consent record is retained.

## Test Case 8

**Description:** Campaign attribution links a tracked interaction to a completed rental.

**Steps:**
1. Have a test customer click a tracked campaign link.
2. Have the same customer complete a rental booking afterward.
3. Generate attribution reporting.
4. Repeat with a different customer who completes a rental without any tracked campaign interaction.

**Expected result:** The first customer's rental is linked back to the originating campaign in the attribution report. The second customer's rental is reported as having no campaign attribution.

## AI Usage Disclaimer
*This document was generated with the assistance of artificial intelligence and should be reviewed by a human for accuracy and completeness.*

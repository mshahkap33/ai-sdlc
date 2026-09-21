# Test Scenario - Campaign Channels

## Document Information
- Author: copilot
- Date:
- Version:

## Table of Contents
- [Test Scenario](#test-scenario)
- [Test Case 1](#test-case-1)
- [Test Case 2](#test-case-2)

## Test Scenario

**Feature to test:** Validate that Marketing can promote rentals across multiple channels (website, app, email, SMS, social media, dealership locations, partner sites) and that content displayed is appropriate per channel, as described in the [Marketing PRD](../../prd/prd-marketing.md#campaign-channels).

**Preconditions:**
- Marketing application/system is running and accessible to a marketing manager.
- A campaign exists in draft state, ready to be published.

## Test Case 1

**Description:** Publishing a campaign to any combination of supported channels.

**Steps:**
1. Log in as a marketing manager.
2. Open a draft campaign.
3. Select a combination of channels (e.g., website, email, and social media).
4. Publish the campaign.

**Expected result:** The campaign is published successfully to all selected channels (website, app, email, SMS, social media, dealership locations, partner sites, or any combination thereof).

## Test Case 2

**Description:** Verifying channel-appropriate content display.

**Steps:**
1. Publish a campaign to multiple channels (e.g., email and SMS).
2. View the campaign content as rendered on the email channel.
3. View the campaign content as rendered on the SMS channel.

**Expected result:** The content displayed on each channel is appropriate to that channel's format (e.g., full rich content on email, concise text on SMS).

## AI Usage Disclaimer
*This document was generated with the assistance of artificial intelligence and should be reviewed by a human for accuracy and completeness.*

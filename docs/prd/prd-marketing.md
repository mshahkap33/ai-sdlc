# PRD - Marketing

## Document Information
- Product / Feature Name: Marketing (Car Rental)
- Author: copilot
- Date:
- Version:

## Table of Contents
- [Overview](#overview)
- [Problem Statement](#problem-statement)
- [Functional Requirements](#functional-requirements)
- [Non-Functional Requirements](#non-functional-requirements)
- [Dependency & Constraints](#dependency--constraints)
- [Success Metrics](#success-metrics)

## Overview

### Background
The company is expanding from car sales into car rental, a new business line with no prior rental experience or dedicated systems. To successfully launch this new line of business, Marketing needs the ability to acquire customers, run promotional campaigns, communicate with renters throughout the rental lifecycle, and report on the effectiveness of these efforts. Today, none of these capabilities exist for rentals, and marketing activity for the existing car-sales business is not connected to rental data.

### Objective
Provide Marketing with the tools and data needed to acquire, engage, and retain car rental customers, while ensuring rental marketing activity is connected to existing car-sales customer records where relevant.

### Goals
- Enable Marketing to identify and target customer segments relevant to car rental.
- Enable Marketing to create and manage promotions (promo codes, discounts, bundles, referral programs, loyalty rewards) with configurable rules.
- Enable automated, consent-based customer communications across the rental lifecycle.
- Provide Marketing with reporting to measure campaign performance, promo usage, and customer value across both rental and sales history.

## Problem Statement
As the company enters the car rental business for the first time, Marketing has no existing tools, data, or processes to acquire and engage rental customers. Without dedicated capabilities, Marketing cannot segment target customers, run promotions, automate lifecycle communications, or measure campaign performance for rentals. This gap affects the Marketing team directly, and indirectly affects Sales (through missed cross-sell opportunities between car sales and rentals) and Operations/Legal (who must retain control over certain communications and consent). Solving this now, at the start of the rental line of business, is important so that customer acquisition, promotions, and reporting capabilities are in place before or as rental operations go live, avoiding a costly retrofit later.

## Functional Requirements

### Customer Segmentation and Targeting

**Title:** Define target customer segments for rentals

**Statement:** As a marketing manager, I want to define and target customer segments for car rentals, so that I can tailor campaigns to individual consumers, corporate clients, travel agencies, insurers, and existing car-sales customers.

**Requirement detail:** The system must allow Marketing to define customer segments (e.g., individual consumers, corporate clients, travel agencies, insurers, existing car-sales customers) and associate campaigns with one or more segments. Segments must be reusable across campaigns.

**Acceptance criteria:**
- Given a marketing manager is creating a campaign, when they select target segments, then they can choose from the predefined segment types (individual consumers, corporate clients, travel agencies, insurers, existing car-sales customers).
- Given a segment is defined, when it is used in multiple campaigns, then the segment definition does not need to be recreated each time.

---

**Title:** Personalize offers using customer data

**Statement:** As a marketing manager, I want to personalize offers using customer data such as location, rental history, car-sales history, and preferences, so that I can increase campaign relevance and conversion.

**Requirement detail:** The system must make available customer attributes (location, rental history, car-sales history, stated preferences) to be used as inputs when building personalized offers or campaign targeting rules.

**Acceptance criteria:**
- Given a customer has prior rental history, when a campaign targeting rule references rental history, then customers matching the rule are included.
- Given a customer has a linked car-sales history, when a campaign targeting rule references car-sales history, then that data is available for targeting.

### Campaign Channels

**Title:** Promote rentals across multiple channels

**Statement:** As a marketing manager, I want to promote rentals through website, app, email, SMS, social media, dealership locations, and partner sites, so that I can reach customers through their preferred channel.

**Requirement detail:** The system must support creating and distributing campaign content across the listed channels, and must allow a campaign to be associated with one or more channels.

**Acceptance criteria:**
- Given a campaign is created, when a marketing manager selects channels, then the campaign can be published to any combination of website, app, email, SMS, social media, dealership locations, and partner sites.
- Given a campaign is published, when it is viewed per channel, then the content displayed is appropriate to the channel selected.

### Promotions

**Title:** Create promotions, discounts, bundles, referral, and loyalty programs

**Statement:** As a marketing manager, I want to create promo codes, discounts, bundles, referral programs, and loyalty rewards, so that I can incentivize rental bookings.

**Requirement detail:** The system must allow Marketing to configure different promotion types: promo codes, percentage/fixed discounts, bundles (e.g., rental + add-ons), referral programs, and loyalty rewards.

**Acceptance criteria:**
- Given a marketing manager creates a promotion, when they select a promotion type, then they can configure it as a promo code, discount, bundle, referral program, or loyalty reward.
- Given a promotion is created, when it is activated, then it becomes available for use according to its configured rules.

---

**Title:** Define promotion eligibility rules

**Statement:** As a marketing manager, I want to define rules governing each promotion, so that promotions apply only to the intended bookings.

**Requirement detail:** The system must allow rules to be configured per promotion, including eligible dates, vehicle categories, locations, and minimum rental length. A promotion must not apply to a booking that does not satisfy all configured rules.

**Acceptance criteria:**
- Given a promotion has eligibility rules configured (dates, vehicle category, location, minimum rental length), when a booking meets all rules, then the promotion is applicable to the booking.
- Given a promotion has eligibility rules configured, when a booking does not meet one or more rules, then the promotion is not applied.

---

**Title:** Determine applicable promotion when multiple could apply

**Statement:** As a marketing manager, I want a defined method to select the applicable promotion when multiple promotions could apply to one reservation, so that customers and staff have a clear, predictable outcome.

**Requirement detail:** The system must not allow multiple promotions to stack on a single reservation unless explicitly configured to be stackable. When more than one non-stackable promotion is eligible, the system must apply a defined selection method (e.g., best discount for the customer, or defined priority order) to choose a single applicable promotion.

**Acceptance criteria:**
- Given more than one eligible promotion applies to a reservation and none are marked stackable, when the reservation is priced, then only one promotion is applied based on the defined selection method.
- Given a promotion is explicitly configured as stackable with another, when both are eligible, then both are applied to the reservation.

---

**Title:** Target campaigns to inventory, location, or demand periods

**Statement:** As a marketing manager, I want to target campaigns to specific inventory, locations, or low-demand periods, so that I can influence utilization where it is most needed.

**Requirement detail:** The system must allow a campaign or promotion to be scoped to specific vehicle inventory, specific rental locations, and/or specific date ranges representing low-demand periods.

**Acceptance criteria:**
- Given a marketing manager scopes a campaign to specific inventory or locations, when a booking is made outside that scope, then the campaign does not apply.
- Given a campaign is scoped to a low-demand date range, when a booking falls within that range, then the campaign is eligible to apply.

### Customer Communications

**Title:** Automate lifecycle communications

**Statement:** As a marketing manager, I want automated messages sent before, during, and after a rental, so that customers receive timely confirmations, reminders, receipts, and surveys without manual effort.

**Requirement detail:** The system must support automated communications triggered by rental lifecycle events, including booking confirmations, pre-rental reminders, receipts, and post-rental surveys.

**Acceptance criteria:**
- Given a rental is booked, when the booking is confirmed, then an automated confirmation message is sent.
- Given a rental is completed, when the post-rental process runs, then a receipt and survey are sent automatically.

---

**Title:** Separate marketing-controlled content from operations/legal-controlled content

**Statement:** As a marketing manager, I want a clear distinction between content marketing can edit and content that must remain controlled by operations/legal, so that regulated or operational content is not altered unintentionally.

**Requirement detail:** The system must distinguish between marketing-owned content (e.g., promotional messaging) and operations/legal-owned content (e.g., contractual terms, legal disclosures), restricting edit permissions accordingly.

**Acceptance criteria:**
- Given a communication template is marked as operations/legal-controlled, when a marketing user attempts to edit it, then the system prevents the edit or restricts it to authorized roles.
- Given a communication template is marked as marketing-controlled, when a marketing user edits it, then the change is allowed.

---

**Title:** Support multi-language communications

**Statement:** As a marketing manager, I want to send communications in multiple languages, so that customers receive messages in their preferred language.

**Requirement detail:** The system must support authoring and sending customer communications in multiple languages, with the ability to select or default the language per customer.

**Acceptance criteria:**
- Given a customer has a preferred language on file, when an automated communication is sent, then it is delivered in that language if a translation exists.
- Given no preferred language is on file, when a communication is sent, then a default language is used.

---

**Title:** Capture consent before marketing communications

**Statement:** As a marketing manager, I want to capture customer consent before sending marketing messages, so that communications comply with applicable requirements.

**Requirement detail:** The system must record customer consent status for marketing communications and must prevent marketing messages from being sent to customers without valid recorded consent.

**Acceptance criteria:**
- Given a customer has not provided consent, when a marketing message is triggered, then the message is not sent.
- Given a customer has provided consent, when a marketing message is triggered, then the message is sent and the consent record is retained.

---

**Title:** Track campaign attribution

**Statement:** As a marketing manager, I want to track campaign attribution from ad click to completed rental, so that I can measure which campaigns drive bookings.

**Requirement detail:** The system must capture attribution data linking a customer's initial campaign interaction (e.g., ad click) through to a completed rental, where technically available.

**Acceptance criteria:**
- Given a customer clicks a tracked campaign link and later completes a rental, when attribution reporting is generated, then the rental is linked back to the originating campaign.
- Given a customer completes a rental without any tracked campaign interaction, when attribution reporting is generated, then the rental is reported as having no campaign attribution.

### Reporting

**Title:** Generate marketing performance reports

**Statement:** As a marketing manager, I want reports on conversion rate, campaign ROI, promo usage, CAC, repeat-rental rate, and CLV, so that I can evaluate and improve marketing effectiveness.

**Requirement detail:** The system must provide reporting covering conversion rate, campaign ROI, promo usage, customer acquisition cost (CAC), repeat-rental rate, and customer lifetime value (CLV).

**Acceptance criteria:**
- Given campaign and booking data exists, when a marketing manager requests a report, then conversion rate, campaign ROI, promo usage, CAC, repeat-rental rate, and CLV are available.
- Given a report is generated, when a specific campaign or promotion is selected as a filter, then the report reflects data for that campaign or promotion only.

---

**Title:** Link rental activity to existing car-sales customer records

**Statement:** As a marketing manager, I want rental activity linked to existing car-sales customer records, so that I have a unified view of each customer across both lines of business.

**Requirement detail:** The system must associate a rental customer record with an existing car-sales customer record when they represent the same individual, using an appropriate matching mechanism.

**Acceptance criteria:**
- Given a rental customer matches an existing car-sales customer, when their profile is viewed, then both rental and car-sales activity are visible together.
- Given a rental customer does not match any existing car-sales customer, when their profile is viewed, then only rental activity is shown until a match is established.

---

**Title:** Flow customer feedback to marketing

**Statement:** As a marketing manager, I want customer feedback and review data to flow to marketing in a timely manner, so that I can respond to sentiment and inform campaign decisions.

**Requirement detail:** The system must make post-rental customer feedback and review data available to Marketing shortly after it is collected.

**Acceptance criteria:**
- Given a customer submits post-rental feedback, when the feedback is recorded, then it becomes visible to marketing reporting within a defined timeframe.
- Given a customer feedback record includes a review score, when marketing reporting is viewed, then the review score is included.

## Non-Functional Requirements


## Dependency & Constraints
- Depends on existing car-sales customer records being accessible for matching and linking rental activity.
- Depends on rental booking, pricing, and inventory data being available to evaluate promotion eligibility.
- Consent capture and communication content controls must align with applicable legal/regulatory requirements; final legal/regulatory rules are outside the scope of this document and must be defined by Operations/Legal.
- Campaign attribution is limited to interactions that can be technically tracked (e.g., tracked links); offline or untrackable interactions cannot be attributed.

## Success Metrics
- Achieve a defined number of new rental bookings per month attributable to marketing campaigns.
- Increase repeat-rental rate among existing car-sales customers by a target percentage.
- Reduce customer acquisition cost (CAC) for rental customers over time.
- Achieve a target promo code/campaign redemption rate on eligible bookings.

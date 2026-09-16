# Product Requirements Document: Marketing

## 1. Overview

This PRD defines the requirements for marketing capabilities supporting the car rental business. It covers customer acquisition and campaign management, customer experience and communications, and marketing reporting. The requirements are derived from stakeholder interviews conducted with the Marketing role.

## 2. Goals

- Enable marketing teams to acquire and retain customers across multiple channels.
- Provide tools to create, manage, and enforce rules for promotions and loyalty programs.
- Ensure customer communications are timely, personalized, compliant, and measurable.
- Provide marketing and business stakeholders with reporting to evaluate campaign performance and customer value.

## 3. Non-Goals

- This document does not define the underlying rental reservation, fleet, or pricing engine functionality except where marketing directly interacts with it (e.g., applying promotions to a reservation).
- Legal/compliance policy authoring is out of scope; this document only specifies where marketing content must respect legal/operations-controlled boundaries.

## 4. Target Customer Segments

The system must support marketing to the following segments:

- Individual consumers
- Corporate clients
- Travel agencies
- Insurers (e.g., replacement-vehicle rentals)
- Existing car-sales customers (cross-sell/upsell from the dealership's sales business)

Each segment may require different messaging, channels, and offers; the system must allow campaigns to be scoped to one or more segments.

## 5. Customer Acquisition and Campaigns

### 5.1 Customer Data for Personalization

To personalize offers, the system must be able to use the following customer data (where consented):

- Location (current, home, or preferred rental location)
- Rental history (past rentals, frequency, vehicle categories used)
- Car-sales history (vehicles purchased, service history, if linked to the dealership's CRM)
- Stated or inferred preferences (vehicle type, price sensitivity, add-ons)

### 5.2 Marketing Channels

Marketing must be able to promote rentals through:

- Website
- Mobile app
- Email
- SMS
- Social media
- Dealership locations (in-person/point-of-sale materials)
- Partner sites

### 5.3 Promotions and Loyalty

Marketing must be able to create and manage:

- Promo codes
- Discounts
- Bundles (e.g., rental + insurance/add-ons)
- Referral programs
- Loyalty rewards

### 5.4 Promotion Rules

Each promotion must support configurable eligibility rules, including:

- Eligible date ranges (start/end, blackout dates)
- Eligible vehicle categories
- Eligible rental locations
- Minimum rental length
- Eligible customer segments

### 5.5 Promotion Stacking

- The system must define whether multiple promotions can be combined on a single reservation.
- By default, promotions should not stack unless explicitly configured to allow it.
- When multiple non-stackable promotions apply, the system must deterministically select the promotion that yields the best value to the customer (or another configurable precedence rule), and must be transparent to the customer about which promotion was applied.

### 5.6 Targeted Campaigns

Marketing must be able to target campaigns based on:

- Specific inventory (e.g., specific vehicle models or units)
- Specific locations
- Low-demand periods (e.g., off-peak dates, underutilized locations)

## 6. Customer Experience and Communications

### 6.1 Automated Messaging

The system must support automated messages at the following points in the customer journey:

- Before rental: booking confirmation, pre-arrival reminders
- During rental: mid-rental check-ins/extensions, roadside assistance notices (where applicable)
- After rental: return confirmation, receipts, post-rental satisfaction surveys

### 6.2 Content Ownership

- Marketing may control promotional and engagement content (offers, newsletters, campaign messaging, surveys).
- Operations/legal must retain control over transactional, contractual, safety, and compliance-related content (e.g., rental agreements, receipts, legal disclosures, recall/safety notices).
- The system must distinguish between marketing-owned and operations/legal-owned content and prevent marketing from editing operations/legal-owned content.

### 6.3 Multi-language Support

- The system must support multi-language communications, allowing customers to receive messages in their preferred language where available.

### 6.4 Consent Management

- The system must capture and store explicit customer consent before sending marketing messages (email, SMS, push, etc.), in compliance with applicable regulations (e.g., opt-in/opt-out preferences).
- The system must allow customers to update or withdraw consent at any time, and marketing communications must respect the current consent status.

### 6.5 Campaign Attribution

- The system must track campaign attribution from initial ad/campaign interaction (e.g., ad click) through to completed rental, to measure campaign effectiveness end-to-end.

## 7. Reporting

### 7.1 Marketing Reports

The system must provide reporting on:

- Conversion rate
- Campaign ROI
- Promo code usage
- Customer Acquisition Cost (CAC)
- Repeat-rental rate
- Customer Lifetime Value (CLV)

### 7.2 Linking Rental and Sales Data

- Rental activity must be linkable to existing car-sales customer records (e.g., via a shared customer ID) to support unified customer profiles and cross-sell reporting.

### 7.3 Customer Feedback and Reviews

- Customer feedback and review data collected after a rental must flow to marketing in near real time (or on a defined, documented cadence) to support timely campaign adjustments and service recovery.

## 8. Open Questions

The following items require further stakeholder input before implementation:

- Exact precedence rules when multiple non-stackable promotions could apply to the same reservation.
- Specific list of languages required for multi-language communications.
- Target latency/cadence for feedback data flowing into marketing reporting.
- Which specific systems (CRM, CDP, ESP) will be used to store consent and customer data.

## 9. Success Metrics

- Increase in campaign-driven bookings (attribution-tracked conversions).
- Improvement in repeat-rental rate and CLV among marketed segments.
- Reduction in CAC over time through improved targeting.
- Compliance rate with consent requirements (zero unconsented marketing sends).

# PRD - Perform Inspections and Capture Evidence

## Document Information
- Product / Feature Name: Perform Inspections and Capture Evidence
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
This PRD elaborates on the "[Perform Inspections and Capture Evidence](./prd-car-management.md#perform-inspections-and-capture-evidence)" functional requirement defined in the [PRD - Car Management](./prd-car-management.md). Our company is expanding from car sales into car rental, a new business line with no prior rental experience or dedicated systems. Renting a vehicle to multiple customers over its lifetime means the condition of every vehicle must be verifiable and disputable at each stage of custody — before it leaves the lot, when it is handed to a customer, and when it comes back. Without a standardized inspection and evidence-capture process, the Company has no reliable way to prove pre-existing damage, identify new damage, or link damage to the correct billing action.

### Objective
Provide Service staff with a standardized way to perform vehicle inspections at every required checkpoint of the rental lifecycle (pre-pickup, handover, and return), capture verifiable evidence for each inspection, and record, classify, and link any identified damage to a billing action.

### Goals
- Standardize the inspection checkpoints required across the rental lifecycle (pre-pickup, handover, return).
- Ensure each inspection captures consistent, verifiable evidence (photos, video, checklist responses, signature, geolocation, timestamp).
- Automatically compare return inspection results against the prior inspection to detect new damage.
- Support classification of damage and link classified damage to a billing action where applicable.
- Reduce disputes over vehicle condition by maintaining a complete, time-stamped inspection history per vehicle.

## Problem Statement
Service staff currently have no standardized process to record and evidence vehicle condition at each stage of the rental lifecycle. This affects:
- **Service staff**, who need a consistent way to perform and record inspections and to identify and classify damage.
- **Delivery/Pickup staff**, who rely on the pre-pickup and handover inspection records to confirm vehicle condition before transferring custody to a customer.
- **Accounting/Billing**, who need classified damage linked to a billing action to charge customers accurately and defend against disputes.
- **Operations managers**, who need a reliable inspection history to resolve condition disputes and monitor damage trends.

This is important now because the Company has no prior rental experience, no existing inspection process, and no historical data to fall back on. Without a standardized, evidence-based inspection process, the business risks unresolvable condition disputes, unbilled or incorrectly billed damage, and an inability to prove vehicle condition at the point of handover or return.

## Functional Requirements

### Define Required Inspection Checkpoints
- **Statement:** As a Service staff member, I want the system to define the required inspection checkpoints across the rental lifecycle, so that no stage of the vehicle's custody goes unverified.
- **Requirement detail:** The system must support at least three inspection checkpoints per rental: pre-pickup (before the vehicle is made available/handed over), handover (at the moment of transfer to the customer), and return (when the customer gives the vehicle back). Each checkpoint must be associated with the vehicle, the rental/reservation, the staff member performing it, and a checkpoint type.
- **Acceptance Criteria:**
  - **Given** a rental is progressing through its lifecycle, **when** each checkpoint (pre-pickup, handover, return) is reached, **then** an inspection record is created and linked to that checkpoint type, the vehicle, and the rental.
  - **Given** an inspection checkpoint has not been completed, **when** staff attempt to advance the rental past that checkpoint (e.g., complete handover without a pre-pickup inspection), **then** the system flags the missing inspection.

### Capture Standardized Inspection Evidence
- **Statement:** As a Service staff member, I want to capture a standard set of evidence during every inspection, so that vehicle condition is verifiable and comparable across checkpoints.
- **Requirement detail:** The system must support capturing photos, video, checklist responses (structured condition items), signature, geolocation, and timestamp for each inspection performed at any checkpoint. All captured evidence must be stored against the specific inspection record.
- **Acceptance Criteria:**
  - **Given** an inspection is being performed at any checkpoint, **when** the inspector submits the inspection, **then** the system requires and stores photos, checklist responses, signature, geolocation, and timestamp before the inspection can be marked complete; video may be attached optionally.
  - **Given** an inspection is submitted without one of the required evidence types, **when** the submission is attempted, **then** the system rejects the submission and identifies the missing evidence.

### Detect New Damage on Return
- **Statement:** As a Service staff member, I want the system to compare the return inspection against the prior inspection, so that any new damage is automatically flagged.
- **Requirement detail:** The system must compare the checklist responses and evidence of the return inspection against the most recent prior inspection (handover, or pre-pickup if handover is unavailable) for the same vehicle and highlight any checklist items or condition areas that changed.
- **Acceptance Criteria:**
  - **Given** a vehicle is returned, **when** the return inspection is performed, **then** the system captures the required evidence and flags any new damage found compared to the prior inspection.
  - **Given** no differences are found between the return inspection and the prior inspection, **when** the comparison runs, **then** the system marks the return inspection as clean with no new damage flagged.

### Record and Classify Damage
- **Statement:** As a Service staff member, I want to record and classify any damage identified during an inspection, so that it can be tracked and appropriately billed.
- **Requirement detail:** The system must allow a damage record to be created from any inspection checkpoint, including a description, affected area, severity classification, and supporting evidence (photo/video) reference. Damage classification must distinguish between pre-existing damage (already known/logged) and new damage.
- **Acceptance Criteria:**
  - **Given** damage is observed during an inspection, **when** staff record it, **then** the system creates a damage record with description, affected area, severity classification, and links it to the inspection and supporting evidence.
  - **Given** a damage record is created, **when** it is classified, **then** the system marks it as either pre-existing or new relative to the vehicle's inspection history.

### Link Classified Damage to Billing
- **Statement:** As a Service staff member, I want classified damage to be linked to a billing action where applicable, so that customers are charged correctly for damage they are responsible for.
- **Requirement detail:** The system must support linking a damage record classified as new (and attributable to the current rental) to a billing action. Damage classified as pre-existing must not automatically generate a billing action.
- **Acceptance Criteria:**
  - **Given** damage is identified during an inspection, **when** it is classified, **then** the system links the damage record to a billing action where applicable.
  - **Given** damage is classified as pre-existing, **when** the classification is saved, **then** no billing action is automatically generated for that damage record.

### Maintain Inspection and Damage History
- **Statement:** As an Operations manager, I want a complete, time-stamped inspection and damage history per vehicle, so that condition disputes can be resolved and damage trends monitored.
- **Requirement detail:** The system must retain all inspection records (with evidence) and damage records for a vehicle across its rental history, queryable by vehicle, rental, checkpoint type, and date range.
- **Acceptance Criteria:**
  - **Given** a vehicle has undergone multiple rentals, **when** its inspection history is queried, **then** all inspection and damage records are returned in chronological order with their associated evidence.
  - **Given** a condition dispute arises for a rental, **when** staff review the inspection history for that rental, **then** the pre-pickup, handover, and return inspection records and any linked damage records are available for review.

## Non-Functional Requirements


## Dependency & Constraints
- This PRD covers only the inspection and evidence-capture functionality (pre-pickup, handover, return inspections, evidence capture, damage classification, and linkage to billing). It does not cover the post-return turnaround task workflow (cleaning, refueling, repair), which is covered by the "Manage Post-Return Turnaround" requirement in the [PRD - Car Management](./prd-car-management.md#manage-post-return-turnaround).
- This PRD does not define the billing/charge calculation logic itself; it only defines that a classified damage record must be linkable to a billing action, which is a dependency on the Accounting capability.
- The digital handover process (signature, ID check, condition checklist at the point of transfer) referenced in "Confirm Handover and Capture Condition" is a related but separate requirement; this PRD focuses specifically on the inspection evidence and damage classification aspects performed at each checkpoint.
- The company has no prior car rental experience or existing inspection systems, so all processes described are net-new and unvalidated by historical operational data.

## Success Metrics
- Achieve 100% completion of required inspections (pre-pickup, handover, return) across all rentals within the first 3 months of launch.
- Reduce disputed damage claims through complete photo/checklist evidence capture at every inspection checkpoint.
- Achieve automatic detection of new damage on return inspections with a target accuracy to be measured once operational data is available.
- Reduce unbilled or misattributed damage charges by ensuring all new, attributable damage is linked to a billing action.

## AI Usage Disclaimer
*This document was generated with the assistance of artificial intelligence and should be reviewed by a human for accuracy and completeness.*

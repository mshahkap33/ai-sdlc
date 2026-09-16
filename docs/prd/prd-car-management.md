# PRD - Car Management

## Document Information
- Product / Feature Name: Car Management
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
Our company is expanding from car sales into car rental, a new business line with no prior rental experience or dedicated systems. Rental operations depend on continuously knowing the state of every vehicle in the fleet — where it is, whether it is available, and whether it is roadworthy — as well as coordinating pickup, delivery, inspection, turnaround, and service activities around each rental. Without a dedicated Car Management capability, staff have no reliable way to track vehicle status, prevent double-booking, capture handover/return conditions, or keep maintenance and compliance current.

### Objective
Provide the Service, Delivery, and Pickup roles with a system to maintain accurate, real-time vehicle data and status, manage pickup/delivery logistics, capture inspection and handover evidence, and track service/maintenance so that vehicles are safe, available, and ready to rent when needed.

### Goals
- Maintain a single source of truth for vehicle data, location, and status across the fleet.
- Prevent double-booking and unsafe rentals by automatically reflecting vehicle availability.
- Support multiple pickup/delivery models with clear scheduling, confirmation, and handover evidence.
- Standardize inspection, damage capture, and turnaround processes to minimize vehicle downtime.
- Keep maintenance, inspections, and compliance documents (registration/insurance/recalls) current and alert staff to issues.
- Give operations staff visibility into daily fleet activity through dashboards and alerts.

## Problem Statement
Service, Delivery, and Pickup staff currently have no dedicated system to manage the rental fleet lifecycle: tracking vehicle data and condition, coordinating pickup/delivery logistics, recording inspections and damage, and scheduling maintenance. This affects:
- **Delivery/Pickup staff**, who need accurate vehicle location, condition, and schedule information to complete handovers.
- **Service/Maintenance staff**, who need visibility into upcoming and overdue maintenance, inspections, and document expirations.
- **Operations managers**, who need a real-time view of fleet utilization and issues (overdue, damaged, or mislocated vehicles).

This is important now because the company is entering the car rental business for the first time and has no existing systems, processes, or historical data to rely on. Without this capability, the business risks double-bookings, unsafe or non-compliant vehicles being rented out, disputed damage claims, and poor fleet utilization from the outset.

## Functional Requirements

### Maintain Vehicle Master Data
- **Statement:** As a Service staff member, I want to maintain core vehicle data (VIN, plate, make/model, mileage, fuel level, location, condition), so that the fleet's identity and condition are accurately tracked.
- **Requirement detail:** The system must store and allow updates to vehicle identity (VIN, plate, make/model, year), operational attributes (mileage, fuel level, current location), and condition notes. Vehicles must be groupable both as a specific unit and by category/class for booking purposes.
- **Acceptance Criteria:**
  - **Given** a new vehicle is added to the fleet, **when** the required identity and condition data is entered, **then** the vehicle record is created and available for grouping into a category/class.
  - **Given** an existing vehicle record, **when** its mileage, fuel level, or location is updated, **then** the change is reflected immediately on the vehicle record.

### Support Vehicle-Level and Category-Level Booking
- **Statement:** As a Delivery/Pickup staff member, I want customers to be able to reserve either a specific vehicle or a vehicle category, so that booking flexibility matches business policy and customer expectations.
- **Requirement detail:** The system must support two reservation modes: exact-vehicle reservation and category/class-only reservation, configurable per policy.
- **Acceptance Criteria:**
  - **Given** a booking policy allows exact-vehicle selection, **when** a customer books a specific VIN/plate, **then** that exact vehicle is held for the reservation.
  - **Given** a booking policy allows only category selection, **when** a customer books a category, **then** any available vehicle in that category may be assigned at fulfillment time.

### Manage Vehicle Status and Availability
- **Statement:** As a Service staff member, I want the system to track and automatically update vehicle status, so that only safe and available vehicles can be booked.
- **Requirement detail:** The system must support vehicle statuses (available, reserved, rented, cleaning, maintenance, damaged, retired) and automatically transition status based on triggering events (e.g., booking confirmed, handover completed, return completed, maintenance scheduled, damage reported). Maintenance schedules, inspections, and registration/insurance expiry or recalls must be able to force a vehicle out of the available pool.
- **Acceptance Criteria:**
  - **Given** a vehicle is booked, **when** the reservation is confirmed, **then** the vehicle status changes to reserved and it cannot be booked by another customer for an overlapping period.
  - **Given** a vehicle's registration, insurance, or inspection has expired, or a recall is open, **when** the expiry/recall condition is detected, **then** the vehicle is automatically marked unavailable until resolved.

### Prevent Double-Booking
- **Statement:** As a Delivery/Pickup staff member, I want the system to prevent double-booking of the same vehicle, so that customers never arrive to find their reserved vehicle unavailable.
- **Requirement detail:** The system must validate vehicle availability against existing reservations and current status before confirming any new booking or vehicle assignment.
- **Acceptance Criteria:**
  - **Given** a vehicle already has a confirmed reservation for a time period, **when** another booking attempt overlaps that period for the same vehicle, **then** the system rejects or blocks the conflicting booking.

### Schedule Pickup and Delivery
- **Statement:** As a Delivery/Pickup staff member, I want to schedule pickup or delivery with all necessary details, so that the handover can be planned and executed correctly.
- **Requirement detail:** The system must support multiple pickup/delivery models (branch, dealership, customer address, airport, hotel, partner location) and capture address, contact information, time window, and vehicle requirements for each scheduled event. Delivery fees may vary by distance, location, vehicle type, or time.
- **Acceptance Criteria:**
  - **Given** a rental requires delivery, **when** staff schedule the delivery, **then** the system records the location, contact, time window, and vehicle requirements, and calculates any applicable delivery fee.
  - **Given** a pickup/delivery is scheduled, **when** the assigned driver/route is determined, **then** the assignment is visible to the delivery/pickup staff.

### Confirm Handover and Capture Condition
- **Statement:** As a Delivery/Pickup staff member, I want to confirm handover completion with digital evidence, so that vehicle condition and custody are clearly documented at the moment of transfer.
- **Requirement detail:** The system must support a digital handover process capturing signature, ID check, photos, condition checklist, and fuel/mileage capture, along with geolocation and timestamp. The system must also handle exception scenarios where the customer is unavailable or the address is incorrect.
- **Acceptance Criteria:**
  - **Given** a vehicle handover is taking place, **when** staff complete the digital handover checklist (signature, ID check, photos, condition, fuel/mileage), **then** the handover record is saved and the vehicle status is updated accordingly.
  - **Given** a customer is unavailable or the delivery address is incorrect, **when** staff flag the exception, **then** the system records the exception and prompts for next steps (e.g., reschedule).

### Perform Inspections and Capture Evidence
- **Statement:** As a Service staff member, I want to record inspections before pickup, at handover, and on return, so that vehicle condition is verifiable at every stage of the rental lifecycle.
- **Requirement detail:** The system must support capturing photos, video, checklist responses, signature, geolocation, and timestamp for each required inspection point, and allow damage to be recorded, classified, and linked to billing.
- **Acceptance Criteria:**
  - **Given** a vehicle is returned, **when** the return inspection is performed, **then** the system captures the required evidence and flags any new damage found compared to the prior inspection.
  - **Given** damage is identified during an inspection, **when** it is classified, **then** the system links the damage record to a billing action where applicable.

### Manage Post-Return Turnaround
- **Statement:** As a Service staff member, I want the system to generate post-return tasks and track turnaround time, so that vehicles return to the rentable pool as quickly as possible.
- **Requirement detail:** The system must generate tasks (cleaning, refueling, repair) after a vehicle is returned, track a target turnaround time, and track lost keys, accessories, or documents.
- **Acceptance Criteria:**
  - **Given** a vehicle is returned, **when** the return inspection is completed, **then** applicable tasks (cleaning, refueling, repair) are automatically created.
  - **Given** all post-return tasks are completed, **when** the vehicle passes final checks, **then** its status is updated to available.

### Schedule and Track Maintenance
- **Statement:** As a Service staff member, I want maintenance to be triggered and tracked based on date, mileage, telematics, or manufacturer schedule, so that vehicles remain safe and compliant.
- **Requirement detail:** The system must support triggering maintenance schedules from multiple sources (date, mileage, telematics, manufacturer schedule) and prioritize urgent repairs, recalls, and safety defects. Alerts must be generated for overdue service, expiring documents, and recalls.
- **Acceptance Criteria:**
  - **Given** a vehicle reaches a mileage or date-based maintenance threshold, **when** the threshold is met, **then** a maintenance alert/work order is generated.
  - **Given** a recall or safety defect is reported for a vehicle, **when** it is logged, **then** the vehicle is flagged for urgent attention and prioritized over routine maintenance.

### View Operational Dashboards and Alerts
- **Statement:** As an Operations manager, I want a daily operational dashboard and targeted alerts, so that I can act quickly on overdue, damaged, or mislocated vehicles.
- **Requirement detail:** The system must provide a dashboard summarizing pickups, returns, late vehicles, maintenance backlog, and utilization, plus fleet-utilization and service reports. Relevant staff must be alerted when a vehicle is overdue, damaged, or mislocated.
- **Acceptance Criteria:**
  - **Given** the daily dashboard is opened, **when** it loads, **then** it displays current pickups, returns, late vehicles, maintenance backlog, and utilization metrics.
  - **Given** a vehicle becomes overdue, damaged, or mislocated, **when** that condition is detected, **then** the appropriate staff are alerted.

## Non-Functional Requirements


## Dependency & Constraints
- This PRD covers only the Car Management role's functionality (fleet/availability, pickup/delivery, inspection/turnaround, service/maintenance, and operational reporting). It does not cover customer-facing booking flows, payment/billing systems, or telematics hardware integration details, which are dependencies to be defined separately.
- Whether maintenance work orders live within this system or an existing third-party service platform is an open decision to be confirmed with stakeholders; this PRD assumes integration with an external service platform is possible but does not mandate it.
- The company has no prior car rental experience or existing rental systems, so all processes described are net-new and unvalidated by historical operational data.

## Success Metrics
- Reduce double-booking incidents to zero within the first 3 months of launch.
- Reduce average vehicle turnaround time (return to rentable) by a target amount (e.g., under 4 hours) once measured.
- Achieve 95%+ compliance rate for up-to-date registration/insurance/inspection status across the fleet.
- Reduce disputed damage claims through complete photo/checklist evidence capture at handover and return.

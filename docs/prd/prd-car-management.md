# PRD - Car Management

## Document Information

| Field | Details |
|---|---|
| **Product / Feature Name** | Car Management (Inventory, Service, Delivery & Pickup) |
| **Author** | Copilot |
| **Date** | |
| **Version** | |

---

## Table of Contents

1. [Overview](#overview)
2. [Problem Statement](#problem-statement)
3. [Functional Requirements](#functional-requirements)
4. [Non-Functional Requirement](#non-functional-requirement)
5. [Dependency & Constraints](#dependency--constraints)
6. [Success Metrics](#success-metrics)

---

## Overview

### Background

Our company is an established player in the car sales business and is now expanding into car rental. Unlike sales, car rental requires ongoing management of a live fleet — tracking availability, condition, location, and service readiness across multiple concurrent bookings. Without a dedicated car management system, the rental operation cannot function reliably.

### Objective

Build a car management module within the car rental system that allows staff to manage the full lifecycle of each rental vehicle, from inventory registration and assignment to bookings, through service scheduling, pickup/return logistics, and incident recording.

### Goals

- Maintain an accurate, real-time inventory of all rental vehicles including their availability, location, and condition.
- Automate service and maintenance scheduling with reminders to minimise vehicle downtime.
- Streamline car assignment to bookings and manage pickup/return processes with proper documentation.
- Support flexible delivery and pickup at customer-chosen locations.
- Enable incident recording and damage tracking throughout the rental lifecycle.
- Provide management reports on fleet utilisation, maintenance, and downtime.

---

## Problem Statement

### User Pain Point / Business Problem

Our car rental operation has no existing system to manage its fleet. Without it, staff must manually track which cars are available, where they are, when they need servicing, and what condition they are in. This leads to double-bookings, missed maintenance, undocumented damage disputes, and an inability to scale the business.

### Who Is Affected?

- **Fleet Managers**: responsible for maintaining and overseeing the entire vehicle inventory.
- **Rental / Counter Staff**: responsible for assigning cars to bookings and handling pickup and return procedures.
- **Drivers / Delivery Staff**: responsible for delivering or collecting cars at customer-specified locations.
- **Customers**: expect a reliable car to be available, in good condition, at the right time and place.
- **Business Analysts / Management**: need visibility into fleet performance through reports.

### Why Is This Important Now?

The car rental business line is launching imminently. Without a car management system in place from the start, the company risks reputational damage from operational failures (wrong cars assigned, missed servicing, damage disputes), legal exposure from undocumented incidents, and an inability to grow the fleet effectively.

---

## Functional Requirements

### FR-01: Car Inventory Management

**Title:** Register and Manage Rental Car Inventory

**Statement:**
**As a** fleet manager, **I want** to register, update, and deactivate vehicles in the system, **so that** I always have an accurate and up-to-date inventory of cars available for rental.

**Requirement Detail:**
The system must allow fleet managers to add new vehicles to the inventory with all relevant attributes. Each vehicle record must be updatable and can be deactivated when the vehicle is retired or sold. The inventory list must support filtering and search.

Vehicle attributes include:
- Vehicle ID / licence plate
- Make, model, year, colour
- Fuel type and transmission type
- Seating capacity
- Current location (branch or zone)
- Current condition (Excellent / Good / Fair / Under Maintenance)
- Current availability status (Available / Reserved / In Rental / Under Maintenance / Retired)
- Odometer reading
- Last service date and next scheduled service date
- Attached photos

**Acceptance Criteria:**

- **Given** a fleet manager is logged in, **when** they submit a new vehicle registration form with all required fields, **then** the vehicle is saved to the inventory with an auto-generated Vehicle ID and status set to "Available."
- **Given** a vehicle record exists, **when** a fleet manager edits any attribute and saves, **then** the record is updated and the change is logged with a timestamp and the editor's identity.
- **Given** a vehicle record exists, **when** a fleet manager deactivates the vehicle, **then** its status changes to "Retired" and it no longer appears in booking assignment searches.
- **Given** a fleet manager views the inventory, **when** they apply a filter (e.g., status = Available, location = Branch A), **then** only vehicles matching all selected filters are shown.

---

### FR-02: Car Information Tracking

**Title:** Track Real-Time Car Location, Condition, and Availability

**Statement:**
**As a** fleet manager, **I want** to view the real-time location, condition, and availability of every vehicle, **so that** I can make informed decisions about assignments, maintenance, and fleet distribution.

**Requirement Detail:**
Each vehicle's current location (branch, customer site, or in-transit), condition, and availability status must be visible in the system. Status changes must be recorded with a timestamp. If the system is integrated with a GPS provider, location updates should be pulled automatically; otherwise, staff can update the location manually.

**Acceptance Criteria:**

- **Given** a vehicle is in the fleet, **when** a staff member opens the vehicle detail page, **then** they can see the current location, condition rating, availability status, and the date/time of the last status update.
- **Given** a vehicle's location is updated manually by a staff member, **when** the update is saved, **then** the new location is reflected immediately in the inventory view and the change is logged.
- **Given** a GPS integration is active for a vehicle, **when** the vehicle moves, **then** its location in the system is updated automatically within the configured refresh interval.
- **Given** a fleet manager views the fleet map/dashboard, **when** they look at a specific vehicle, **then** they can see its current map position and status.

---

### FR-03: Car Assignment to Rental Bookings

**Title:** Assign a Car to a Confirmed Rental Booking

**Statement:**
**As a** rental staff member, **I want** to assign a specific available vehicle to a confirmed booking, **so that** the customer's reservation is fulfilled with a suitable car.

**Requirement Detail:**
When a booking is confirmed, a staff member (or the system automatically) must assign an available vehicle that matches the booking's requested car category, pickup location, and date range. The system must prevent assigning a car that is already reserved, under maintenance, or not available for the requested period. Once assigned, the car's status must be updated to "Reserved."

**Acceptance Criteria:**

- **Given** a confirmed booking exists with a specified car category and pickup date, **when** a staff member initiates car assignment, **then** the system shows only vehicles that are available, match the requested category, and are located at or can be transferred to the pickup location.
- **Given** a staff member selects a vehicle and confirms assignment, **when** the assignment is saved, **then** the vehicle's status is updated to "Reserved" and is no longer offered for other bookings overlapping the same dates.
- **Given** a staff member attempts to assign a vehicle that is already reserved or under maintenance, **when** they try to confirm the assignment, **then** the system shows an error message and does not permit the assignment.
- **Given** a booking is cancelled, **when** the cancellation is processed, **then** any assigned vehicle's status is automatically reverted to "Available."

---

### FR-04: Service and Maintenance Schedule Management

**Title:** Manage Car Service Schedules with Automated Reminders

**Statement:**
**As a** fleet manager, **I want** to schedule and track vehicle service and maintenance events with automated reminders, **so that** no service is missed and cars remain safe and roadworthy.

**Requirement Detail:**
The system must allow fleet managers to create, edit, and close service records for each vehicle. Service types include routine service (mileage or time-based), safety inspections, tyre changes, and ad-hoc repairs. The system must automatically generate a reminder notification to the fleet manager when a scheduled service date is approaching (configurable threshold, e.g., 7 days before). When a car is placed "Under Maintenance," it must be automatically removed from the available pool.

**Acceptance Criteria:**

- **Given** a fleet manager opens a vehicle record, **when** they create a new service entry with a scheduled date and type, **then** the entry is saved and linked to that vehicle.
- **Given** a service date is within the configured reminder window, **when** the system runs its daily check, **then** an in-system notification (and optionally an email) is sent to the fleet manager listing vehicles due for service.
- **Given** a vehicle is marked as "Under Maintenance", **when** a staff member attempts to assign it to a booking, **then** the system prevents the assignment and displays an appropriate message.
- **Given** a service is completed, **when** the fleet manager marks it as done and enters the completion date and odometer reading, **then** the vehicle's condition and last service date are updated, and the next service date is recalculated based on the service interval rules.

---

### FR-05: Pickup and Return Logistics Management

**Title:** Manage Car Pickup and Return Processes

**Statement:**
**As a** rental staff member, **I want** to record and manage the details of car pickup and return events, **so that** handover is documented, timely, and any condition changes are captured.

**Requirement Detail:**
At pickup, the system must guide staff through a structured checklist covering the vehicle's condition, fuel level, odometer reading, and any pre-existing damage notes. At return, the same checklist is repeated and compared to the pickup record to identify any new damage. Both events must be timestamped and linked to the rental booking.

**Acceptance Criteria:**

- **Given** a rental is due for pickup, **when** a staff member opens the pickup checklist for the booking, **then** they are presented with fields for odometer reading, fuel level, condition rating, and a pre-existing damage notes field, along with the option to upload photos.
- **Given** all required pickup fields are completed and submitted, **when** the staff member confirms pickup, **then** the booking status changes to "Active," the vehicle status changes to "In Rental," and a pickup record with timestamp is saved.
- **Given** a rental is due for return, **when** a staff member opens the return checklist, **then** the pre-existing conditions from the pickup record are displayed alongside new condition fields for comparison.
- **Given** the return checklist is completed and submitted, **when** the staff member confirms return, **then** the booking status changes to "Completed," the vehicle status reverts to "Available" (or "Under Maintenance" if damage is noted), and a return record with timestamp is saved.

---

### FR-06: Pickup and Return Documentation

**Title:** Capture Documentation at Pickup and Return

**Statement:**
**As a** rental staff member, **I want** to capture photos, damage reports, and customer signatures at pickup and return, **so that** there is a clear, legally defensible record of the vehicle's condition at both handover points.

**Requirement Detail:**
The system must support photo uploads (minimum 4 angles: front, rear, driver-side, passenger-side) and free-text or structured damage notation (location on car diagram + severity) at both pickup and return. A digital signature capture must be provided for the customer to sign off on the pickup and return condition report. All documents must be stored and linked to the rental booking record.

**Acceptance Criteria:**

- **Given** a staff member is completing the pickup checklist, **when** they tap/click "Add Photo," **then** they can upload one or more images from the device, each labelled with the angle/position.
- **Given** photos are uploaded and condition is noted, **when** the staff member presents the digital signature field to the customer, **then** the customer can sign on-screen (or via a digital signature pad), and the signature is captured and stored against the booking.
- **Given** the condition report and signature are saved, **when** the customer requests a copy, **then** the system can generate a PDF summary of the condition report including photos, notes, and signature.
- **Given** a return is completed with new damage noted, **when** the return record is saved, **then** the damage details are automatically flagged for follow-up and visible in the fleet manager's damage report queue.

---

### FR-07: Incident Recording During Rental

**Title:** Record Incidents During a Rental Period

**Statement:**
**As a** rental staff member, **I want** to log incidents such as accidents or breakdowns that occur during an active rental, **so that** the company can respond appropriately and maintain an accurate history for each vehicle.

**Requirement Detail:**
Any incident reported during an active rental must be loggable in the system against the booking and the vehicle. An incident record must capture: incident type (accident, breakdown, theft, other), date/time, location, description, third-party details (if applicable), and supporting photos. Incidents must trigger a notification to the fleet manager. The vehicle may be automatically set to "Under Maintenance" upon incident logging.

**Acceptance Criteria:**

- **Given** a rental is active, **when** a staff member creates a new incident record linked to the booking, **then** they are presented with a form capturing incident type, date/time, location, description, third-party information, and photo attachments.
- **Given** an incident record is submitted, **when** it is saved, **then** a notification is sent to the fleet manager and the incident is visible on the vehicle's history timeline.
- **Given** the incident type is "Accident" or "Breakdown", **when** the incident is saved, **then** the vehicle's availability status is automatically updated to "Under Maintenance" until cleared by the fleet manager.
- **Given** a vehicle has one or more incident records, **when** a fleet manager views the vehicle detail page, **then** all incident records are visible in a chronological history section.

---

### FR-08: Delivery and Pickup at Customer-Chosen Locations

**Title:** Manage Car Delivery and Collection at Customer Locations

**Statement:**
**As a** customer, **I want** to request that the rental car be delivered to or collected from a location of my choosing, **so that** I do not have to visit a branch for pickup or return.

**Requirement Detail:**
The system must allow customers to specify a delivery address and/or a collection address at the time of booking or via a pre-rental amendment. These requests must be communicated to and managed by delivery/driver staff through task assignments in the system. The system must support a configurable delivery service radius and applicable surcharge logic. Delivery tasks must be assigned to a specific staff member/driver and tracked through a lifecycle: Pending → En Route → Delivered.

**Acceptance Criteria:**

- **Given** a customer is creating or amending a booking, **when** they opt for delivery service and enter an address, **then** the system validates that the address is within the allowed service radius and displays any applicable delivery surcharge.
- **Given** a delivery address is outside the configured service radius, **when** the customer submits the request, **then** the system shows an error indicating delivery is unavailable to that location.
- **Given** a delivery task is created, **when** a fleet manager assigns it to a driver, **then** the driver receives an in-system notification with the delivery address, booking details, and scheduled delivery time.
- **Given** a driver marks a delivery task as "Delivered", **when** the update is saved, **then** the booking's pickup status is updated, the customer is notified, and the vehicle's status is updated to "In Rental."

---

### FR-09: Fleet Management and GPS Integration

**Title:** Integrate with External Fleet Management and GPS Systems

**Statement:**
**As a** fleet manager, **I want** the car rental system to integrate with our existing fleet management or GPS tracking systems, **so that** I have a unified view of all vehicle data without manual duplication.

**Requirement Detail:**
The system must support integration with third-party GPS/telematics providers via a configurable API connection. Vehicle location data from GPS should automatically update the vehicle record. Odometer readings or engine hour data (where available) from telematics should be usable to trigger service reminders. The integration must be configurable per vehicle (since not all vehicles may have GPS devices).

**Acceptance Criteria:**

- **Given** a GPS integration is configured for a vehicle, **when** the GPS provider sends a location update, **then** the vehicle's location in the system is updated within the configured sync interval (e.g., every 5 minutes).
- **Given** a telematics provider reports that a vehicle has reached a mileage-based service threshold, **when** the system receives this data, **then** a service reminder is automatically created or triggered for that vehicle.
- **Given** a vehicle does not have a GPS device configured, **when** staff view the vehicle record, **then** location and telematics fields show "Manual Update Required" and staff can update them manually.
- **Given** a fleet manager configures the GPS integration settings, **when** they test the connection, **then** the system validates connectivity and reports success or failure with a diagnostic message.

---

### FR-10: Fleet Utilisation, Downtime, and Maintenance Reports

**Title:** Generate Vehicle Utilisation, Downtime, and Maintenance Reports

**Statement:**
**As a** fleet manager, **I want** to generate reports on vehicle utilisation, downtime, and maintenance history, **so that** I can make data-driven decisions about the fleet's performance and investment.

**Requirement Detail:**
The system must provide a reporting module where fleet managers and business analysts can generate and export standard reports. Report types must include at minimum:
- **Utilisation Report**: percentage of time each vehicle (or the whole fleet) was in active rental vs available, per period.
- **Downtime Report**: time vehicles were unavailable due to maintenance, incidents, or other non-rental reasons.
- **Maintenance Cost Report**: service and repair costs per vehicle over a selected period.
- **Incident Report**: list of incidents by vehicle, date range, type, and resolution status.

Reports must be filterable by date range, vehicle, branch, and category, and exportable as CSV or PDF.

**Acceptance Criteria:**

- **Given** a fleet manager opens the reports module, **when** they select "Utilisation Report" and set a date range, **then** the system generates a report showing each vehicle's rental days vs total available days as a percentage.
- **Given** a report is generated, **when** the manager clicks "Export CSV" or "Export PDF," **then** the file is downloaded containing all displayed data in the chosen format.
- **Given** a fleet manager filters the downtime report by branch, **when** the filter is applied, **then** only vehicles assigned to that branch are included in the results.
- **Given** an incident has been marked as resolved, **when** it appears in the Incident Report, **then** its resolution status and closure date are correctly displayed.

---

## Non-Functional Requirement

_(To be defined)_

---

## Dependency & Constraints

- **Desktop Web Only**: The car management module is initially scoped for desktop web browsers. Mobile-responsive support is out of scope for this phase.
- **Rental Booking System Dependency**: Car management depends on an existing or concurrently developed booking/reservation module. Vehicle assignment and rental lifecycle tracking (FR-03, FR-05) require booking records to exist.
- **GPS Integration is Optional**: GPS/telematics integration (FR-09) is a configurable enhancement. Core vehicle tracking via manual updates must work independently when no GPS device is attached.
- **Digital Signature**: Digital signature capture (FR-06) requires compatible hardware (touch screen or signature pad) at rental branches. This is a physical infrastructure dependency outside the system's scope.
- **User Authentication & Roles**: Access to car management features is restricted by user role (Fleet Manager, Rental Staff, Driver, Business Analyst). A user authentication and role management system must be in place.
- **Existing Fleet Management Systems**: Integration with any existing fleet management tools used by the sales division is out of scope for Phase 1. Data migration from those systems is a separate workstream.

---

## Success Metrics

- **Fleet Utilisation Rate**: Achieve a measurable fleet utilisation rate above 70% within 6 months of launch, tracked via the utilisation report.
- **Reduction in Missed Services**: Reduce missed or overdue vehicle service events by 90% within 3 months, compared to the manual baseline (zero automated reminders today).
- **Damage Dispute Resolution Time**: Reduce average time to resolve damage disputes by 50% through complete photo and signature documentation at pickup/return.
- **Car Assignment Accuracy**: Achieve 99%+ accuracy in car assignments (no double-bookings or assignment of unavailable vehicles) from go-live.
- **Incident Recording Compliance**: 100% of incidents reported during active rentals are logged in the system within 24 hours.
- **Delivery Task On-Time Rate**: Achieve 95% on-time delivery/collection rate for customer-location delivery tasks within 6 months of launching the delivery service.
- **Report Adoption**: Fleet managers generate and use fleet reports at least weekly within 1 month of launch.

# Database Design – Assign Car to Rental Booking

## Overview

This document describes the database tables required to support the **Assign Car to Rental Booking** feature (US-CM-03). It covers the rental bookings and the assignment relationship between cars and bookings, together with supporting reference data.

> **Note:** The `cars` and `car_service_schedules` tables are part of the consolidated Car Management database design and are defined in:
> 📄 [database-design-car-management.md](./database-design-car-management.md)
>
> This document references those tables but does not redefine them.

---

## Entity Relationship Diagram

```mermaid
erDiagram
    CARS {
        UUID          id                  PK
        VARCHAR(20)   licence_plate
        VARCHAR(100)  make
        VARCHAR(100)  model
        SMALLINT      year
        VARCHAR(50)   colour
        VARCHAR(20)   fuel_type
        SMALLINT      seating_capacity
        VARCHAR(255)  current_location
        SMALLINT      condition_rating
        VARCHAR(30)   status
        BOOLEAN       is_active
        DATE          next_service_date
        TIMESTAMP     created_at
        TIMESTAMP     updated_at
    }

    CAR_SERVICE_SCHEDULES {
        UUID        id                       PK
        UUID        car_id                   FK
        VARCHAR     service_type
        DATE        scheduled_date
        DECIMAL     estimated_downtime_hours
        VARCHAR     service_provider
        VARCHAR     status
        TEXT        notes
        TIMESTAMP   completed_at
        TIMESTAMP   created_at
        TIMESTAMP   updated_at
    }

    LOCATIONS {
        uuid        id            PK
        varchar     name
        text        address
        varchar     city
        varchar     country
        varchar     type
        timestamp   created_at
        timestamp   updated_at
    }

    USERS {
        uuid        id            PK
        varchar     username      UK
        varchar     full_name
        varchar     email         UK
        varchar     role
        boolean     is_active
        timestamp   created_at
        timestamp   updated_at
    }

    CUSTOMERS {
        uuid        id            PK
        varchar     full_name
        varchar     email         UK
        varchar     phone
        timestamp   created_at
        timestamp   updated_at
    }

    BOOKINGS {
        uuid        id                  PK
        uuid        customer_id         FK
        uuid        pickup_location_id  FK
        uuid        return_location_id  FK
        date        start_date
        date        end_date
        varchar     status
        timestamp   created_at
        timestamp   updated_at
    }

    CAR_BOOKING_ASSIGNMENTS {
        uuid        id              PK
        uuid        booking_id      FK
        uuid        car_id          FK
        uuid        assigned_by     FK
        timestamp   assigned_at
        timestamp   unassigned_at
        boolean     is_current
        timestamp   created_at
        timestamp   updated_at
    }

    CAR_STATUS_HISTORY {
        uuid        id              PK
        uuid        car_id          FK
        varchar     previous_status
        varchar     new_status
        uuid        changed_by      FK
        text        reason
        timestamp   changed_at
    }

    CARS            ||--o{  CAR_SERVICE_SCHEDULES       : "has"
    LOCATIONS       ||--o{  BOOKINGS                    : "pickup location"
    LOCATIONS       ||--o{  BOOKINGS                    : "return location"
    CUSTOMERS       ||--o{  BOOKINGS                    : "makes"
    BOOKINGS        ||--o{  CAR_BOOKING_ASSIGNMENTS     : "assigned via"
    CARS            ||--o{  CAR_BOOKING_ASSIGNMENTS     : "assigned to"
    USERS           ||--o{  CAR_BOOKING_ASSIGNMENTS     : "assigned by"
    CARS            ||--o{  CAR_STATUS_HISTORY          : "tracks"
    USERS           ||--o{  CAR_STATUS_HISTORY          : "changed by"
```

---

## Table Descriptions

### `cars` and `car_service_schedules`

These tables are defined in the consolidated Car Management database design:
📄 [database-design-car-management.md](./database-design-car-management.md)

Key points relevant to this feature:
- `cars.status` values used here: `available`, `reserved`, `rented`, `in_service`, `unavailable`, `inactive`.
- `cars.current_location` is a `VARCHAR(255)` text field that is matched against the booking's pickup location name.
- `cars.is_active` must be `TRUE` for a car to be eligible for assignment.
- `car_service_schedules.scheduled_date` and `car_service_schedules.estimated_downtime_hours` are used to compute the service blocking period when filtering eligible cars.

---

### `locations`

Represents physical locations (depots, airports, etc.) used as pickup or return points for bookings.

| Column     | Type        | Constraints      | Description                                      |
|------------|-------------|------------------|--------------------------------------------------|
| id         | UUID        | PK               | Unique identifier                                |
| name       | VARCHAR     | NOT NULL         | Human-readable name (e.g., "City Centre Depot")  |
| address    | TEXT        | NOT NULL         | Street address                                   |
| city       | VARCHAR     | NOT NULL         | City                                             |
| country    | VARCHAR     | NOT NULL         | Country                                          |
| type       | VARCHAR     | NOT NULL         | Location type (e.g., `depot`, `airport`, `other`)|
| created_at | TIMESTAMP   | NOT NULL         | Record creation timestamp                        |
| updated_at | TIMESTAMP   | NOT NULL         | Record last-update timestamp                     |

---

### `users`

Represents internal system users (fleet managers, operations staff, field agents). Managed by the User Management system.

| Column     | Type      | Constraints      | Description                                                   |
|------------|-----------|------------------|---------------------------------------------------------------|
| id         | UUID      | PK               | Unique identifier                                             |
| username   | VARCHAR   | NOT NULL, UNIQUE | Login username                                                |
| full_name  | VARCHAR   | NOT NULL         | Display name                                                  |
| email      | VARCHAR   | NOT NULL, UNIQUE | Email address                                                 |
| role       | VARCHAR   | NOT NULL         | Role: `fleet_manager`, `operations_staff`, `field_agent`      |
| is_active  | BOOLEAN   | NOT NULL         | Whether the user account is active                            |
| created_at | TIMESTAMP | NOT NULL         | Record creation timestamp                                     |
| updated_at | TIMESTAMP | NOT NULL         | Record last-update timestamp                                  |

---

### `customers`

Represents customers who make rental bookings. Managed by the Booking system.

| Column     | Type      | Constraints      | Description                        |
|------------|-----------|------------------|------------------------------------|
| id         | UUID      | PK               | Unique identifier                  |
| full_name  | VARCHAR   | NOT NULL         | Customer's full name               |
| email      | VARCHAR   | NOT NULL, UNIQUE | Customer's email address           |
| phone      | VARCHAR   |                  | Customer's phone number            |
| created_at | TIMESTAMP | NOT NULL         | Record creation timestamp          |
| updated_at | TIMESTAMP | NOT NULL         | Record last-update timestamp       |

---

### `bookings`

Represents confirmed rental bookings. Managed by the Booking system; referenced here as the anchor for car assignments.

| Column             | Type      | Constraints            | Description                                                                     |
|--------------------|-----------|------------------------|---------------------------------------------------------------------------------|
| id                 | UUID      | PK                     | Unique identifier                                                               |
| customer_id        | UUID      | FK → customers         | The customer who made the booking                                               |
| pickup_location_id | UUID      | FK → locations         | Where the customer will collect the car                                         |
| return_location_id | UUID      | FK → locations         | Where the customer will return the car                                          |
| start_date         | DATE      | NOT NULL               | Start date of the rental period                                                 |
| end_date           | DATE      | NOT NULL               | End date of the rental period                                                   |
| status             | VARCHAR   | NOT NULL               | Booking status: `confirmed`, `active`, `completed`, `cancelled`                 |
| created_at         | TIMESTAMP | NOT NULL               | Record creation timestamp                                                       |
| updated_at         | TIMESTAMP | NOT NULL               | Record last-update timestamp                                                    |

---

### `car_booking_assignments`

Records the assignment of a car to a booking. Only one assignment may be active at a time per booking (enforced by `UNIQUE (booking_id) WHERE is_current = TRUE`).

| Column         | Type      | Constraints               | Description                                                                             |
|----------------|-----------|---------------------------|-----------------------------------------------------------------------------------------|
| id             | UUID      | PK                        | Unique identifier                                                                       |
| booking_id     | UUID      | FK → bookings, NOT NULL   | The booking the car is assigned to                                                      |
| car_id         | UUID      | FK → cars, NOT NULL       | The car assigned to the booking                                                         |
| assigned_by    | UUID      | FK → users, NOT NULL      | The operations staff member who made the assignment                                     |
| assigned_at    | TIMESTAMP | NOT NULL                  | When the assignment was made                                                            |
| unassigned_at  | TIMESTAMP |                           | When the assignment was removed (NULL if still active)                                  |
| is_current     | BOOLEAN   | NOT NULL, default TRUE    | TRUE if this is the active assignment for the booking; FALSE for historical assignments |
| created_at     | TIMESTAMP | NOT NULL                  | Record creation timestamp                                                               |
| updated_at     | TIMESTAMP | NOT NULL                  | Record last-update timestamp                                                            |

**Indexes & Constraints:**
- Partial unique index: `UNIQUE (booking_id) WHERE is_current = TRUE` — prevents more than one active assignment per booking.
- Index on `(car_id, is_current)` — speeds up conflict-detection queries across active car assignments.

---

### `car_status_history`

Audit trail of all car status changes, including those triggered by assignment and unassignment events.

| Column          | Type      | Constraints         | Description                                       |
|-----------------|-----------|---------------------|---------------------------------------------------|
| id              | UUID      | PK                  | Unique identifier                                 |
| car_id          | UUID      | FK → cars, NOT NULL | The car whose status changed                      |
| previous_status | VARCHAR   | NOT NULL            | Status before the change                          |
| new_status      | VARCHAR   | NOT NULL            | Status after the change                           |
| changed_by      | UUID      | FK → users          | User who triggered the change (NULL if automated) |
| reason          | TEXT      |                     | Optional description of why the status changed    |
| changed_at      | TIMESTAMP | NOT NULL            | When the change occurred                          |

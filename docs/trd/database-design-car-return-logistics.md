# Database Design – Car Return Logistics

## Entity Relationship Overview

The return logistics feature introduces four tables: `return_record`, `return_photo`, `return_signature`, and `damage_report`. They relate to the existing `bookings` and `cars` tables, and reference the `users` table for audit purposes.

```
bookings ──< return_record >── cars
                  │
                  ├──< return_photo
                  │
                  ├──── return_signature
                  │
                  └──── damage_report
```

---

## Tables

### `return_record`

Stores the structured data collected during a car return handover at the end of a rental booking.

| Column | Type | Constraints | Description |
|---|---|---|---|
| `id` | UUID | PK, NOT NULL | Unique identifier for the return record |
| `booking_id` | UUID | FK → `bookings.id`, NOT NULL, UNIQUE | The rental booking this return is for |
| `car_id` | UUID | FK → `cars.id`, NOT NULL | The car being returned |
| `return_datetime` | TIMESTAMP WITH TIME ZONE | NOT NULL | Recorded date and time of return |
| `return_location` | VARCHAR(500) | NOT NULL | Address or location description of the return |
| `fuel_level` | ENUM(`empty`, `quarter`, `half`, `three_quarter`, `full`) | NOT NULL | Fuel level at time of return |
| `odometer_reading` | INTEGER | NOT NULL, CHECK ≥ 0 | Odometer reading (km) at time of return |
| `condition_notes` | TEXT | NULLABLE | Free-text notes on the car's condition at return |
| `damage_found` | BOOLEAN | NOT NULL, DEFAULT FALSE | Whether damage was recorded during the return check |
| `damage_report_id` | UUID | FK → `damage_report.id`, NULLABLE | Reference to the damage report, if damage was found |
| `signature_id` | UUID | FK → `return_signature.id`, NULLABLE | Reference to the captured customer signature |
| `preparation_period_minutes` | INTEGER | NULLABLE, CHECK ≥ 0 | Optional cleaning/preparation hold before car returns to Available (in minutes) |
| `status` | ENUM(`draft`, `confirmed`) | NOT NULL, DEFAULT `draft` | Lifecycle status of the return record |
| `created_by` | UUID | FK → `users.id`, NOT NULL | User who initiated the return |
| `created_at` | TIMESTAMP WITH TIME ZONE | NOT NULL, DEFAULT NOW() | Record creation timestamp |
| `confirmed_at` | TIMESTAMP WITH TIME ZONE | NULLABLE | Timestamp when the return was confirmed |
| `confirmed_by` | UUID | FK → `users.id`, NULLABLE | User who confirmed the return |

**Indexes:**
- `booking_id` (UNIQUE) — ensures at most one return record per booking
- `car_id` — supports queries for a car's return history
- `status` — supports filtering by draft/confirmed records
- `damage_found` — supports filtering records that have damage

---

### `return_photo`

Stores references to photos uploaded as part of the return condition check. One return record may have many photos.

| Column | Type | Constraints | Description |
|---|---|---|---|
| `id` | UUID | PK, NOT NULL | Unique identifier for the photo |
| `return_record_id` | UUID | FK → `return_record.id`, NOT NULL | The return record this photo belongs to |
| `storage_reference` | VARCHAR(1000) | NOT NULL | File storage path or URL for the photo |
| `file_name` | VARCHAR(255) | NOT NULL | Original filename at time of upload |
| `file_size_bytes` | INTEGER | NOT NULL, CHECK > 0 | File size in bytes |
| `mime_type` | VARCHAR(50) | NOT NULL | MIME type (e.g., `image/jpeg`, `image/png`) |
| `uploaded_at` | TIMESTAMP WITH TIME ZONE | NOT NULL, DEFAULT NOW() | Timestamp of upload |
| `uploaded_by` | UUID | FK → `users.id`, NOT NULL | User who uploaded the photo |

**Indexes:**
- `return_record_id` — supports fetching all photos for a given return record

---

### `return_signature`

Stores a reference to the customer's digital or scanned signature captured at the time of return handover.

| Column | Type | Constraints | Description |
|---|---|---|---|
| `id` | UUID | PK, NOT NULL | Unique identifier for the signature |
| `storage_reference` | VARCHAR(1000) | NOT NULL | File storage path or URL for the signature image |
| `captured_at` | TIMESTAMP WITH TIME ZONE | NOT NULL | Timestamp when the signature was captured |
| `captured_by` | UUID | FK → `users.id`, NOT NULL | User who recorded the signature |

**Indexes:**
- None beyond the primary key; referenced by `return_record.signature_id`

---

### `damage_report`

Records details of damage identified during the return check. Generated automatically when `damage_found` is set to `true` on a return record.

| Column | Type | Constraints | Description |
|---|---|---|---|
| `id` | UUID | PK, NOT NULL | Unique identifier for the damage report |
| `return_record_id` | UUID | FK → `return_record.id`, NOT NULL, UNIQUE | The return record that triggered this report |
| `booking_id` | UUID | FK → `bookings.id`, NOT NULL | The booking associated with the damage |
| `car_id` | UUID | FK → `cars.id`, NOT NULL | The car on which damage was found |
| `description` | TEXT | NOT NULL | Damage description provided by the field agent |
| `review_status` | ENUM(`pending`, `under_review`, `resolved`) | NOT NULL, DEFAULT `pending` | Current review status of the damage report |
| `reviewed_by` | UUID | FK → `users.id`, NULLABLE | Fleet manager or staff member who reviewed the report |
| `reviewed_at` | TIMESTAMP WITH TIME ZONE | NULLABLE | Timestamp when the review was completed |
| `resolution_notes` | TEXT | NULLABLE | Notes recorded when the damage report is resolved |
| `created_at` | TIMESTAMP WITH TIME ZONE | NOT NULL, DEFAULT NOW() | Record creation timestamp |

**Indexes:**
- `return_record_id` (UNIQUE) — ensures at most one damage report per return record
- `car_id` — supports queries for a car's damage history
- `booking_id` — supports queries for bookings with damage
- `review_status` — supports filtering reports by review state

---

## Relationships

| Relationship | Cardinality | Description |
|---|---|---|
| `bookings` → `return_record` | 1 : 0..1 | A booking may have at most one return record |
| `cars` → `return_record` | 1 : 0..N | A car may appear in multiple return records over time |
| `return_record` → `return_photo` | 1 : 0..N | A return record may have zero or more photos while in draft; at least one photo is required before it can be confirmed |
| `return_record` → `return_signature` | 1 : 0..1 | A return record has no signature while in draft; exactly one signature is required before it can be confirmed |
| `return_record` → `damage_report` | 1 : 0..1 | A damage report is created only when `damage_found` is `true` on the return record |
| `damage_report` → `cars` | N : 1 | Multiple damage reports may reference the same car over its lifetime |
| `damage_report` → `bookings` | N : 1 | Multiple damage reports may reference the same booking (in edge cases) — typically one per booking |
| `users` → `return_record` | 1 : 0..N | A user may create or confirm many return records |
| `users` → `return_photo` | 1 : 0..N | A user may upload many photos |
| `users` → `return_signature` | 1 : 0..N | A user may capture many signatures |
| `users` → `damage_report` | 1 : 0..N | A user (fleet manager) may review many damage reports |

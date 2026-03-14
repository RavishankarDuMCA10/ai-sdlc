# Database Design - View Car Inventory

The `cars` table and its related `locations` table used by this feature are defined in the consolidated Car Management database design document.

👉 [`cars` table — database-design-car-management.md#cars](./database-design-car-management.md#cars)

👉 [`locations` table — database-design-car-management.md#locations](./database-design-car-management.md#locations)

The `cars` table references `locations` via the `location_id` foreign key, which resolves to the current physical location of the vehicle (depot, airport, etc.).

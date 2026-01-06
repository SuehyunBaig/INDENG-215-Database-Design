## OLTP Implementation Using MongoDB & MongoDB Compass (GUI)

Here we implement another OLTP system using MongoDB, one of the most popular NoSQL databases. Each collection represents a key business entity or item and consists of documents including the attributes required for daily operations.
The **document-oriented design** of MongoDB groups related data logically while maintaining relationships across collections using referenced identifiers (e.g., `CustomerID`, `ArtistID`, `InstructorID`). 
This approach has an edge over relational databases in its flexibility (no schemas) and readability (no joins needed)

---

## Revenue Management Collections

These collections support **ticket sales, lesson sessions, and customer activity**, enabling accurate revenue tracking, reconciliation, and reporting.

### `customers`
Stores customer profile information and serves as the primary reference for ticket purchases, lessons, and product purchases.

**Key attributes**
- `CustomerID`
- `first_name`
- `last_name`
- `email`

---

### `artists`
Stores information about performers associated with shows, listening room sessions, and album products.

**Key attributes**
- `ArtistID`
- `stage_name`
- `genre`

---

### `shows`
Stores concert event information and links each show to one or more performing artists.

**Key attributes**
- `ShowID`
- `show_name`
- `show_date`
- `artist_ids` (list of associated `ArtistID`s)

---

### `tickets`
Stores ticket sales transactions at the customer and show level. Ticket quantity and price are stored directly to support revenue reporting and artist compensation analysis.

**Key attributes**
- `TicketID`
- `CustomerID`
- `ShowID`
- `quantity`
- `price`

---

### `lessons`
Stores lesson session data to track lesson revenue, customer participation, and instructor workloads.

**Key attributes**
- `SessionID`
- `InstructorID`
- `CustomerID`
- `instrument_type`
- `lesson_date`
- `lesson_price`

---

## Expense and Budget Control Collections

These collections support **operational expense tracking**, enabling budget monitoring and vendor-level analysis.

### `vendors`
Stores vendor information so expenses can be categorized and analyzed by vendor type.

**Key attributes**
- `VendorID`
- `vendor_type`

---

### `transactions`
Stores individual expense transactions paid to vendors. Corporate card information is embedded directly in each transaction document since it is used only for reference during expense tracking.

**Key attributes**
- `TransactionID`
- `VendorID`
- `transaction_amount`
- `transaction_date`
- `card_number`

---

## Scheduling and Resource Allocation Collections

These collections support **staffing and space management** to prevent scheduling conflicts and track resource usage.

### `instructors`
Stores instructor information to associate lesson sessions with instructors and track salary-related costs.

**Key attributes**
- `InstructorID`
- `first_name`
- `last_name`
- `salary`

---

### `listeningRooms`
Stores listening room sessions and the artists assigned to each session, enabling room usage and scheduling analysis.

**Key attributes**
- `RoomID`
- `ArtistID`
- `listening_date`

---

## Product Inventory Collections

These collections support **retail operations and inventory management** for albums and merchandise.

### `products`
Stores all items sold by the concert hall. A `product_type` attribute distinguishes between albums and merchandise, with additional attributes included only when applicable.

**Common attributes**
- `ProductID`
- `product_name`
- `product_type`
- `price`
- `inventory_quantity`

**Album-specific attributes**
- `ArtistID`
- `release_year`
- `title`

**Merchandise-specific attributes**
- `merch_type`

---

### `purchases`
Stores customer product purchases to track units sold and revenue by product and customer.

**Key attributes**
- `PurchaseID`
- `CustomerID`
- `ProductID`
- `quantity`
- `unit_price`
- `purchase_date`

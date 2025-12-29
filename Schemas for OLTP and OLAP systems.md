## Schemas - OLTP and OLAP

### Transactional Data (OLTP)

Transactional tables support the concert hall’s **daily operations**, including revenue tracking, expense management, scheduling, and inventory control.

#### Revenue Management
Tracks ticket sales, lessons, and merchandise purchases at the transaction level.

**Core Tables:**
- `Customer` (CustomerID, FName, LName, Email)
- `Show` (ShowID, ShowName, ShowDate)
- `Ticket` (CustomerID FK, ShowID FK, Quantity, Price)
- `Artist` (ArtistID, StageName, Genre)
- `Lesson` (SessionID, InstructorID FK, CustomerID FK, InstrumentType, LessonDate, LessonPrice)
---

#### Expense & Budget Control
Tracks operational payments made to vendors using corporate credit cards.

**Core Tables:**
- `Vendor` (VendorID, VendorType)
- `CorporateCard` (CardNum)
- `Transaction` (VendorID FK, CardNum FK, TransactionAmount, Date)
---

#### Scheduling & Resource Allocation
Manages instructors and room usage for lessons and listening sessions.

**Core Tables:**
- `Instructor` (InstructorID, FName, LName, Salary)
- `ListeningRoom` (RoomID, ArtistID FK, ListeningDate)
---

#### Product Inventory
Supports retail operations for albums and merchandise.

**Core Tables:**
- `Product` (ProductID, ItemType, ItemPrice)
- `Album` (ProductID FK, ArtistID FK, ReleaseYear, Title)
- `Merch` (ProductID FK, MerchType)
---

### Archival Data (OLAP)

Historical data is stored separately to enable **analytical queries** without impacting transactional performance. Two fact tables are modeled using a **Star Schema**.

#### Fact Table 1: Ticket Sales

**Fact Table:**
- `Fact_TicketSales` (TicketSaleKey, DateKey FK, CustomerID FK, ShowID FK, ArtistID FK, TicketQuantity, UnitPrice, TotalRevenue)

**Dimensions:**
- `Dim_Date` (DateKey, Date, Year, Month, Day, DayOfWeek)
- `Dim_ConcertGoer` (ConcertGoerKey, CustomerID SK, FName, LName, Email)
- `Dim_Show` (ShowKey, ShowID FK, ShowName, OriginalShowDate)
- `Dim_Artist` (ArtistKey, ArtistID FK, StageName, Genre)

---

#### Fact Table 2: Lesson Sales

**Fact Table:**
- `Fact_LessonSales` (LessonSaleKey, DateKey FK, InstructorID FK, CustomerID FK, InstrumentType, LessonRevenue)

**Dimensions:**
- `Dim_Date` (DateKey, Date, Year, Month, Day, DayOfWeek)
- `Dim_Instructor` (InstructorKey, InstructorID SK, FName, LName, AnnualSalary)
- `Dim_Student` (StudentKey, CustomerID SK, FName,_

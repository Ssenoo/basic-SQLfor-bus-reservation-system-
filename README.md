# 🚌 Bus Transportation System — Database Project

A relational database project designed and implemented using **Microsoft SQL Server (T-SQL)** as part of a Database Systems course. The system models a bus transportation network, managing users, drivers, buses, routes, and trips with full referential integrity.

---

## 📋 Table of Contents

- [Project Overview](#project-overview)
- [Database Schema](#database-schema)
- [Entity-Relationship Diagram](#entity-relationship-diagram)
- [File Structure](#file-structure)
- [How to Run](#how-to-run)
- [Sample Data](#sample-data)
- [Query Categories](#query-categories)

---

## Project Overview

This project implements a complete relational database for a **bus transportation management system**. It supports:

- Registering **users** and **drivers**
- Managing **buses** with assigned drivers
- Defining **routes** with pickup and drop-off locations
- Scheduling **trips** with status tracking (Active / Cancelled / Completed)
- Linking **users to trips** they have booked

---

## Database Schema

The database consists of **6 tables** with the following structure:

### `userss`
| Column | Type | Constraints |
|--------|------|-------------|
| userID | INT | PRIMARY KEY, IDENTITY |
| firstname | VARCHAR(10) | NOT NULL |
| lastname | VARCHAR(10) | — |
| Email | VARCHAR(40) | UNIQUE |
| phonenum | INT | UNIQUE, NOT NULL |
| passwordd | VARCHAR(20) | NOT NULL |

### `driver`
| Column | Type | Constraints |
|--------|------|-------------|
| driverID | INT | PRIMARY KEY, IDENTITY |
| firstname | VARCHAR(10) | NOT NULL |
| lastname | VARCHAR(10) | — |
| Email | VARCHAR(30) | UNIQUE, NOT NULL |
| licensenum | INT | UNIQUE, NOT NULL |

### `Bus`
| Column | Type | Constraints |
|--------|------|-------------|
| BusId | INT | PRIMARY KEY, IDENTITY |
| capacity | INT | NOT NULL |
| model | VARCHAR(10) | — |
| manufacturer | VARCHAR(30) | — |
| registrationnum | INT | UNIQUE, NOT NULL |
| DriverID | INT | FK → driver(driverID) |

### `Routess`
| Column | Type | Constraints |
|--------|------|-------------|
| RoutesId | INT | PRIMARY KEY, IDENTITY |
| routename | VARCHAR(30) | NOT NULL |
| pickuplocation | VARCHAR(30) | NOT NULL |
| dropofflocation | VARCHAR(30) | NOT NULL |
| busID | INT | FK → Bus(BusId) |

### `trips`
| Column | Type | Constraints |
|--------|------|-------------|
| TripsId | INT | PRIMARY KEY, IDENTITY |
| statuss | VARCHAR | NOT NULL (Active / Cancelled / Completed) |
| numofseats | VARCHAR(10) | NOT NULL |
| pickuptime | DATETIME | NOT NULL |
| dropofftime | DATETIME | NOT NULL |
| busID | INT | FK → Bus(BusId) |
| routeID | INT | FK → Routess(RoutesId) |

### `user_trips` *(Junction Table)*
| Column | Type | Constraints |
|--------|------|-------------|
| userID | INT | PK + FK → userss(userID) |
| tripsID | INT | PK + FK → trips(TripsId) |

---

## Entity-Relationship Diagram

> See `erd.png` and `schema.png` in the root directory, or refer to `project erd&schema.pdf` for the full ERD and schema documentation.

**Relationships:**
- One **Driver** → One **Bus** (1:1 assignment)
- One **Bus** → Many **Routes** (1:N)
- One **Bus** → Many **Trips** (1:N)
- One **Route** → Many **Trips** (1:N)
- Many **Users** ↔ Many **Trips** via `user_trips` (M:N)

---

## File Structure

```
updated/
│
├── project.sql              # Main SQL script: DDL (CREATE) + DML (INSERT)
├── project.txt              # Plain-text copy of the SQL script
├── erd.png                  # Entity-Relationship Diagram
├── schema.png               # Database schema diagram
├── project erd&schema.pdf   # Full ERD & schema documentation (PDF)
│
├── db state pics/           # Screenshots of table data after inserts
│   ├── bus .png
│   ├── driver.png
│   ├── routess.png
│   ├── trips.png
│   ├── user_trips.png
│   └── userss.png
│
└── Queries/                 # SQL query result screenshots organized by type
    ├── Aggregate functions/
    │   ├── avg.png
    │   ├── count.png
    │   ├── max.png
    │   ├── min.png
    │   └── sum.png
    │
    ├── joins/
    │   ├── inner,png.png
    │   ├── left.png
    │   └── right.png
    │
    ├── order by/
    │   ├── bus order by capacity.png
    │   ├── driver order by lastname.png
    │   ├── routes order by pickup location.png
    │   ├── trips order by num of seats.png
    │   ├── users order by firstname.png
    │   └── users_trips order by userID desc.png
    │
    ├── string pattern/
    │   ├── bus.png
    │   ├── driver.png
    │   ├── routes.png
    │   ├── trips.png
    │   └── userss.png
    │
    └── where cond/
        ├── bus.png
        ├── driver.png
        ├── routes.png
        ├── trips.png
        └── userss .png
```

---

## How to Run

1. Open **SQL Server Management Studio (SSMS)**.
2. Connect to your local SQL Server instance.
3. Create a new database:
   ```sql
   CREATE DATABASE BusTransportDB;
   USE BusTransportDB;
   ```
4. Open `project.sql` and execute it in full.
   - This will create all 6 tables and populate them with 20 sample records each.

---

## Sample Data

The script seeds the database with **20 records per table**:

| Table | Records |
|-------|---------|
| userss | 20 users |
| driver | 20 drivers |
| Bus | 20 buses (Volvo, Mercedes, Toyota, Scania, MAN) |
| Routess | 20 routes across Egyptian cities |
| trips | 20 trips (mix of Active, Cancelled, Completed) |
| user_trips | 20 bookings (1 user per trip) |

**Cities covered:** Cairo, Giza, Alexandria, Luxor, Aswan, Mansoura, Fayoum, Minya, Ismailia, Suez, Tanta, Zagazig, Beni Suef, Sohag, Damietta, Port Said, Sharm El Sheikh, Hurghada.

---

## Query Categories

The `Queries/` folder contains result screenshots for the following SQL query types:

| Category | Description |
|----------|-------------|
| **Aggregate Functions** | `COUNT`, `SUM`, `AVG`, `MIN`, `MAX` applied on table columns |
| **JOINs** | `INNER JOIN`, `LEFT JOIN`, `RIGHT JOIN` across related tables |
| **ORDER BY** | Sorting results on each table by relevant columns (ASC/DESC) |
| **String Pattern** | `LIKE`-based pattern matching on text fields |
| **WHERE Condition** | Filtered queries using conditional expressions |

---

## Technologies Used

- **Database:** Microsoft SQL Server (T-SQL)
- **Tool:** SQL Server Management Studio (SSMS)
- **Language:** SQL (DDL + DML)

---

*Database Systems Project — Term 3*

---
title: "Pakistan Airlines Management System"
description: "Production-ready desktop enterprise automation system for airline operations — Java Swing GUI with JDBC-backed MySQL relational storage."
summary: "Java SE desktop application for flight booking, passenger management, ticket cancellation, and administrative reporting at Sukkur IBA University."
date: 2025-04-15
ShowBreadCrumbs: true
ShowToc: true
ShowReadingTime: true
sourceUrl: "https://github.com/Yousif-Sahito"
cover:
  image: "/images/projects/ams.png"
  alt: "Pakistan Airlines Management System dashboard"
techStack: "Java SE · Swing · AWT · JDBC · MySQL"
---

## Overview

The **Pakistan Airlines Management System** (Airport Management System) is a production-ready, desktop-based enterprise automation platform built with **Java SE** using an object-oriented client-server architecture with modular GUI components and relational MySQL storage.

Developed as an academic milestone at **Sukkur IBA University, Pakistan**, under the guidance of **Dr. Engr. Zainab Umair Kamangar**.

| Metadata | Detail |
|----------|--------|
| Project Status | Production Ready (Academic Milestone Accomplished) |
| Target Domain | Desktop-Based Enterprise Automation |
| Platform | Java SE (Standard Edition) |
| Architecture | Object-Oriented Client-Server (Modular GUI & Relational Storage) |
| Co-Authors | Muhammad Yousif, Muhammad Ibrahim, Saif-Ur-Rehman |

---

## 🏗️ System Architecture

The project features a **decoupled, modular desktop pattern**. The application layer handles presentation logic and user-event listening through pure Java code, while database connectivity layers manage data synchronization via explicit driver connections.

```
┌────────────────────────────────────────────────────────┐
│           Java Swing + AWT Presentation Tier           │
│  - Event Listeners (java.awt.event.*)                  │
│  - Custom UI Components (PillButton, RoundButton)     │
│  - Visual Form Submissions & Data Rendering            │
└───────────────────────────┬────────────────────────────┘
                            │
                            │ Synchronous Java Objects / Data Vectors
                            ▼
┌────────────────────────────────────────────────────────┐
│                Core Business Logic Tier                │
│  - Object-Oriented Paradigms (Encapsulation, Poly)     │
│  - Exception Handling & Structural Input Validation    │
│  - Helper Query Compilation Layer                      │
└───────────────────────────┬────────────────────────────┘
                            │
                            │ Java Database Connectivity (JDBC API)
                            ▼
┌────────────────────────────────────────────────────────┐
│            ConnectionClass Gateway Driver              │
│  - mysql-connector-j.jar Core Bridge                   │
│  - PreparedStatement / ResultSet Serialization         │
└───────────────────────────┬────────────────────────────┘
                            │
                            │ Native SQL Queries
                            ▼
┌────────────────────────────────────────────────────────┐
│                MySQL Database Cluster                  │
│  - Relational Schema Network (5 Core System Tables)    │
└────────────────────────────────────────────────────────┘
```

### Technology Stack

| Layer | Technology |
|-------|------------|
| Language | Java SE — OOP (encapsulation, inheritance, polymorphism, abstraction) |
| UI Framework | Java Swing (`javax.swing.*`) + AWT (`java.awt.*`) |
| Database | MySQL — relational mappings across 5 core tables |
| Connector | JDBC via `java.sql.*` + `mysql-connector-j.jar` |
| Utilities | `java.util.*` (ArrayList, HashMap), `java.text.*` (SimpleDateFormat) |

---

## 📁 Project Directory Layout (`AMS/`)

```
AMS/
├── HomePage.java              # Main dashboard and navigation controller
├── Login.java                 # User authentication and session validation
├── ViewPassenger.java         # Passenger data display grid and search matrix
├── BookFlight.java            # Interactive flight booking engine
├── UpdatePassenger.java       # Passenger profile modification forms
├── FlightZone.java            # Regional flight details management system
├── CancelFlight.java          # Ticket cancellation and transaction parsing
├── ViewBookedFlight.java      # Active reservation logging grid
├── ViewCanceledTicket.java    # Historic cancellation record archive
├── ConnectionClass.java       # Centralized JDBC connection handler
└── Helper Classes/
    ├── GradientPanel.java     # Custom background visual renderer
    ├── ShadowLabel.java       # Decorative visual component module
    ├── PillButton.java        # Custom visual component module
    └── RoundButton.java       # Custom visual component module
```

---

## 🔎 Core Functional Modules

### User Authentication System

Restricts access using database-verified credentials. Inputs are matched against the `signup` table using parameterized drivers before granting interface access.

### Passenger Management

Coordinates CRUD operations and filtering of customer profiles. Enables additions, searches, and visual mapping of user records using a clean `JTable` grid.

### Flight Booking System

Facilitates seat reservations by tracking real-time availability, ticket classes, and dynamic pricing. Automatically issues unique Ticket IDs, matching passengers with respective flight identifiers.

### Flight Management

Gives operators full administrative control over flight parameters — flight codes, route sources, destinations, times, seating caps, and operational statuses like **Delayed** or **On Time**.

### Ticket & Cancellation Management

Provides structured flows to cancel trips, record cancellation logs, and automatically update reservation metrics from **Success** to **Cancelled**.

### Administrative Overview & Reporting

Centralized reporting tools pull database indicators to generate operational summaries covering passenger tracking, financial details, and route logs from a unified view.

---

## 🗄️ Relational Database Architecture

The data layout is built on a relational MySQL structure ensuring **referential integrity** across related schemas.

```
                       ┌──────────────────┐
                       │      signup      │
                       └──────────────────┘
                 Stores Authentication Details

 ┌──────────────────┐        1        N ┌──────────────────┐
 │    passenger     ├──────────────────>│     booking      │
 └────────┬─────────┘                   └────────┬─────────┘
          │ 1                                    │ N
          │                                      │
          │ 1                                    │ 1
          ▼                                      ▼
 ┌──────────────────┐                   ┌──────────────────┐
 │      flight      │                   │      cancel      │
 └──────────────────┘                   └──────────────────┘
Contains Routes & Schedules             Logs Revoked Invoices
```

### Core Tables

| Table | Purpose |
|-------|---------|
| `signup` | Operational access credentials for admin and desk operators |
| `passenger` | Demographic profiles — names, contact info, identity numbers |
| `flight` | Airline schedules — sources, destinations, routes, capacities |
| `booking` | Connects passengers to flights with distinct ticket IDs |
| `cancel` | Cancellation history logs with timestamps and reasons |

---

## 🎨 UI Implementation Details

The design follows modern GUI practices using **custom UI components** that extend basic Swing modules.

- **Dynamic Visual Rendering:** `GradientPanel` provides smooth background color transitions inspired by airline branding
- **Custom Geometric Modifiers:** `PillButton` and `RoundButton` deliver modern, rounded interactive controls
- **Depth Filtering:** `ShadowLabel` adds depth underneath text markers for readability over colorful backgrounds
- **Initial View Guardrail:** Form layouts keep selection boxes empty before database queries, ensuring UI state matches the database during setup

---

## ⚙️ Engineering Challenges Overcome

| Challenge | Solution |
|-----------|----------|
| Secure CRUD Integration | Replaced basic SQL with `PreparedStatement` logic — SQL injection protection |
| State Alignment | Automated refresh hooks keep database in sync when switching between booking and cancellation grids |
| Concurrent Component Layouts | Managed layout managers and event handlers to resolve UI resizing across monitor resolutions |

---

## 🚀 Future Enhancements Roadmap

- **Online Payment Gateway:** Stripe or PayPal APIs for online ticket purchases
- **Automated Notifications:** SMTP email and SMS services for schedule changes, delay alerts, and transaction summaries
- **Cloud Infrastructure:** Migration to AWS RDS or Azure MySQL for cross-regional access and scalability
- **Cross-Platform Portability:** Expand into multi-tenant mobile applications or web portals

---

## 👥 Engineering Ownership

| Role | Engineer | Scope |
|------|----------|-------|
| Co-Author | Muhammad Yousif (Yousif-Sahito) | Core modules, JDBC integration, UI components |
| Co-Author | Muhammad Ibrahim | Business logic, database schema |
| Co-Author | Saif-Ur-Rehman | GUI design, testing |
| Project Guide | Dr. Engr. Zainab Umair Kamangar | Academic supervision |

---

## 🔗 Explore More

- [View on GitHub](https://github.com/Yousif-Sahito)
- [Hostel Mess Management System](/projects/hostel-mess-management/)
- [E-commerce Platform](/projects/ecommerce-platform/)

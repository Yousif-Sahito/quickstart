---
title: "Hostel Mess Management System"
description: "Production-ready cross-platform hostel mess management platform with Flutter frontend, Node.js REST API, and MySQL — security score 8.6/10."
summary: "Decoupled client-server system for hostel operations: meal tracking, billing, room allocation, RBAC, and FCM notifications across Android, iOS, Web, and Desktop."
date: 2026-01-15
ShowBreadCrumbs: true
ShowToc: true
ShowReadingTime: true
sourceUrl: "https://github.com/Yousif-Sahito"
cover:
  image: "/images/projects/hms.png"
  alt: "Hostel Mess Management System login screen"
techStack: "Flutter · Node.js · Express · MySQL · Prisma · JWT · Firebase FCM"
---

## Overview

The **Hostel Mess Management System** is a production-ready, decoupled client-server platform for managing hostel mess operations, member lifecycle, room allocation, attendance, billing, and financial analytics.

Built with a **Flutter cross-platform frontend** and a **Node.js + Express REST API** backed by **MySQL**, the system supports 12 core operational modules across **ADMIN** and **MEMBER** roles with JWT-authenticated stateless sessions.

| Metric | Value |
|--------|-------|
| Project Status | Production Ready |
| Build Integrity | Clean & Passing |
| Security Score | **8.6 / 10** |
| Codebase Size | 10,000+ Lines of Code |
| Architecture | Decoupled Client-Server (RESTful API) |

---

## 🏗️ System Architecture

The system uses a modern **tiered architecture** separating presentation, business logic, and data storage.

```
┌────────────────────────────────────────────────────────┐
│               Flutter Mobile Frontend                  │
│       (Cross-Platform: Android, iOS, Web, Desktop)     │
└───────────────────────────┬────────────────────────────┘
                            │
                            │ HTTP / REST API (JWT Authenticated)
                            ▼
┌────────────────────────────────────────────────────────┐
│               Node.js + Express Backend                │
│    - Middleware Filters (Helmet, CORS, Rate Limit)     │
│    - Session Tokens (JWT Validation Layer)             │
│    - Database Gateway (Prisma ORM Client)              │
└───────────────────────────┬────────────────────────────┘
                            │
                            │ Fluent Queries / Connection Pool
                            ▼
┌────────────────────────────────────────────────────────┐
│                     MySQL Database                     │
│    - Relational Schemas (8+ Core Normalized Tables)    │
└────────────────────────────────────────────────────────┘
```

### Technology Stack

| Layer | Technology |
|-------|------------|
| Frontend | Flutter (Dart) — Android, iOS, Web, Desktop |
| Backend | Node.js (v16+) + Express |
| Database | MySQL (v8.0+) — 8+ normalized tables |
| ORM | Prisma — type-safe queries, SQLi protection |
| Auth | JWT (7-day expiration) |
| Cryptography | Bcrypt (work factor 10) |
| Push Notifications | Firebase Cloud Messaging (FCM v4+) |

---

## 🔎 Core Functional Modules

The platform is divided into **12 core operational modules** based on administrative or member user roles.

### User Administration & Security

- **Role-Based Access Control (RBAC):** Restricts execution paths to `ADMIN` or `MEMBER` scopes
- **Cryptographic Account Registration:** Signups, verification token mailings, secure login
- **Self-Service Recovery:** Password-reset with 15-minute transient verification states

### Hostel Allocation & Operations

- **Room Inventory Management:** Tracks occupancies, bedding capacities, residential distributions
- **Member Lifecycle Directory:** Student profiles, room indices, financial parameters
- **Daily Attendance Tracking:** Historical logbooks for active resident statuses

### Mess Tracking & Consumption

- **Per-Member Meal Loggers:** Real-time day-to-day food consumption counts
- **Mess Off Scheduling:** Pause allocations during trips with automatic bill adjustments
- **Helper Charges Matrix:** Operational expenses distributed across billing pools

### Financial Ledgers & Analytics

- **Automated Billing Engine:** Compiles periodic invoices from meal and maintenance variables
- **Transaction Processing:** Payment logging, outstanding dues, digital vouchers
- **Dashboard Analytics:** Financial summaries, meal statistics, room utilization charts

---

## 🛡️ Production Hardening & Security

The system satisfies high industry security benchmarks with an audit score of **8.6/10**.

| Guardrail | Implementation |
|-----------|----------------|
| HTTP Hardening | Helmet.js — X-XSS-Protection, HSTS, X-Frame-Options |
| Network Control | CORS restrictions blocking arbitrary origins |
| Rate Limiting | 1000 req/15 min global; 5 req/15 min on auth routes |
| Error Sanitization | Centralized middleware hides stack traces in production |
| SQL Injection | Prisma ORM parameterized queries |

---

## 🌐 RESTful API Architecture

Decoupled endpoints protected by JWT authentication interceptor.

### Authentication (`/api/auth`)

| Method | Route | Description |
|--------|-------|-------------|
| POST | `/login` | Verify credentials, return signed JWT |
| POST | `/register` | Add unverified account record |
| POST | `/forgot-password` | Generate 15-minute recovery link |
| POST | `/reset-password` | Process tokens to update credentials |
| POST | `/verify-email` | Confirm email ownership |
| POST | `/update-fcm-token` | Update FCM registration token |
| POST | `/delete-account` | (Protected) Securely purge user data |

### Administrative (`/api/members`, `/api/rooms`)

- **GET/POST** `/api/members` — (Admin) Fetch or append member listings
- **PUT/DELETE** `/api/members/:id` — (Admin) Modify or remove profiles
- **GET/POST** `/api/rooms` — Control room configurations

### Operational Routes

- **GET/POST** `/api/meals` — Meal entry tracking by date and count
- **GET/POST** `/api/bills` — Automated period statements
- **POST** `/api/payments` — Log payment transactions
- **POST** `/api/messoff` — Schedule mess-off intervals

---

## 📊 Performance & Reliability Benchmarks

| Metric | Target Threshold |
|--------|------------------|
| API Response Latency | Under 200ms per query |
| Database Processing | Under 100ms per operation |
| Client Initialization | Under 3 seconds to interactive |
| FCM Delivery Success | Exceeding 99% |
| Operational Uptime | 99.5% availability |
| Database Redundancy | Daily automated backups |
| System Error Rate | Below 0.1% |

---

## 🚀 Deployment Blueprint

### Backend Setup Pipeline

1. **Environment Variables:** `DATABASE_URL`, `JWT_SECRET` (via `openssl rand -base64 32`), admin configs
2. **Schema Provisioning:**
   ```bash
   npm run prisma:generate   # Pre-compile Prisma SDK Client
   npm run prisma:push       # Apply model schemas to MySQL
   ```
3. **Database Seeding:** `npm run seed:admin` and `npm run seed:settings`

### Frontend API Mapping

| Platform | Endpoint |
|----------|----------|
| Android Emulator | `http://10.0.2.2:5000/api` |
| iOS Simulator | `http://localhost:5000/api` |
| Physical Devices | Local network IP over Wi-Fi |

---

## 👥 Engineering Ownership

| Role | Engineer | Scope |
|------|----------|-------|
| Full-Stack Developer | Muhammad Yousif (Yousif-Sahito) | Flutter frontend, Node.js API, Prisma schema, security hardening, deployment |

---

## 🔗 Explore More

- [View on GitHub](https://github.com/Yousif-Sahito)
- [E-commerce Platform](/projects/ecommerce-platform/)
- [Air line management System](/projects/ams/)

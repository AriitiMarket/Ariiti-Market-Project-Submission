# Ariiti Market — Project Submission

**Project Name:** Ariiti Market  
**Description:** A local-first Ethiopian e-commerce marketplace, merchant operations, and delivery management platform.

---

## 📌 Project Overview

**Ariiti Market** connects buyers, local sellers, delivery providers, and platform administrators into a unified digital commerce ecosystem. Tailored specifically for local market operational realities, the platform provides seamless multi-vendor commerce, verified merchant onboarding, dynamic location and route logistics, and end-to-end order tracking.

---

## 🎥 Project Demonstration

- **Demonstration Video:** `[INSERT YOUR YOUTUBE OR GOOGLE DRIVE LINK HERE]`
  > *Note: If sharing via YouTube, set video visibility to **Unlisted**. If using Google Drive, set access to **"Anyone with the link can view"**.*

---

## 📦 Source Code Repositories

The project codebase is architectured into three specialized, production-ready repositories:

| Repository | GitHub Link | Description |
| :--- | :--- | :--- |
| **Backend Microservices** | [AriitiMarket/backend-micro](https://github.com/AriitiMarket/backend-micro) | Node.js microservices (`identity-service`, `commerce-service`, `delivery-service`), API Gateway, **polyglot persistence** (PostgreSQL + MongoDB), and automated **GitHub Actions CI/CD pipelines**. |
| **Marketplace Web Frontend** | [AriitiMarket/aritii-seller-buyer-web](https://github.com/AriitiMarket/aritii-seller-buyer-web) | Customer storefront and Seller Center portal (product catalog, dynamic search, cart & checkout, escrow payments, order management). |
| **Admin & Operations Console** | [AriitiMarket/Aritii-admin-web](https://github.com/AriitiMarket/Aritii-admin-web) | Dedicated management portal for Super Admins and Operations Admins (order monitoring, merchant verification, SLA tracking, disputes). |

---

## 🏗️ System Architecture & Polyglot Database Design

Ariiti Market implements a **polyglot persistence model**, selecting the optimal database engine for each domain service:

```
                                  ┌────────────────────────────────┐
                                  │   Clients / Web Applications   │
                                  └───────────────┬────────────────┘
                                                  │
                         ┌────────────────────────┴────────────────────────┐
                         │                                                 │
                         ▼                                                 ▼
          ┌─────────────────────────────┐                   ┌─────────────────────────────┐
          │  Customer & Seller Portal   │                   │    Admin Operations Web     │
          │ (aritii-seller-buyer-web)   │                   │      (Aritii-admin-web)     │
          └──────────────┬──────────────┘                   └──────────────┬──────────────┘
                         │                                                 │
                         └────────────────────────┬────────────────────────┘
                                                  │
                                                  ▼
                                    ┌───────────────────────────┐
                                    │    Central API Gateway    │
                                    │ (aritii-gateway / Express)│
                                    └─────────────┬─────────────┘
                                                  │
                         ┌────────────────────────┼────────────────────────┐
                         │                        │                        │
                         ▼                        ▼                        ▼
          ┌────────────────────────┐┌────────────────────────┐┌────────────────────────┐
          │    Identity Service    ││    Commerce Service    ││    Delivery Service    │
          │   (Auth, RBAC, Users)  ││ (Products, Orders, Pay)││ (Zones, Routes, Dispatch)
          └───────────┬────────────┘└───────────┬────────────┘└───────────┬────────────┘
                      │                         │                         │
                      │                         └────────────┬────────────┘
                      ▼                                      ▼
          ┌────────────────────────┐             ┌────────────────────────┐
          │  PostgreSQL Database   │             │    MongoDB Database    │
          │                        │             │                        │
          │ • Users & Credentials  │             │ • Product Catalogs     │
          │ • Admin Roles & Scopes │             │ • Orders & Carts       │
          │ • Granular Permissions │             │ • GeoJSON Zones/Routes │
          │ • Relational Integrity │             │ • Flexible Doc Schemas │
          └────────────────────────┘             └────────────────────────┘
                                       │
                                       ▼
                         ┌───────────────────────────┐
                         │   Redis (Cache & Rate)    │
                         └───────────────────────────┘
```

---

## 💾 Database Strategy & Service Breakdown

### 1. Identity Service — **PostgreSQL**
- **Engine:** PostgreSQL (`pg` connection pool)
- **Role:** Central authentication, user accounts, and Role-Based Access Control (RBAC).
- **Why PostgreSQL?**
  - Requires strict relational integrity, ACID compliance, and foreign key constraints between `users`, `admin_roles`, and `admin_user_roles`.
  - Ensures robust transactional security for password hashing (bcrypt), verification statuses, and fine-grained administrative scoping.

### 2. Commerce Service — **MongoDB**
- **Engine:** MongoDB with Mongoose ODM
- **Role:** Businesses, multi-shop management, dynamic product catalog, inventory, multi-item shopping carts, wishlists, and escrow orders.
- **Why MongoDB?**
  - Highly dynamic, nested data structures: products have varying attributes (variants, media, specifications, ratings).
  - Fast read/write performance for high-traffic customer browsing, carts, and order snapshots.

### 3. Delivery & Logistics Service — **MongoDB**
- **Engine:** MongoDB with Mongoose ODM & GeoJSON support
- **Role:** Delivery location hierarchies, ports, dynamic delivery zones, provider assignment, delivery requests, and live package tracking.
- **Why MongoDB?**
  - Native geospatial indexing (`2dsphere`), GeoJSON polygons/coordinates for location mapping and route calculation.
  - Flexibility to evolve logistics milestones, dispatch events, and provider status tracking without rigid schema migrations.

---

## 🚀 DevOps: Continuous Integration & Continuous Deployment (CI/CD)

The backend microservices repository features a production-grade automated CI/CD pipeline powered by **GitHub Actions** and **Render Deploy Hooks**:

### 1. Continuous Integration (CI) — `.github/workflows/ci.yml`
- **Automated Validation:** Triggers on all pushes and pull requests across `main` and feature branches.
- **Microservices Unit & Integration Tests:** Runs test suites automatically across Node.js 20 runtime environments.
- **Shared Packages & Architecture Validation:** Validates dependency consistency and architectural boundaries across internal shared libraries (`@aritii/authz`, `@aritii/database`, `@aritii/internal-auth`, `@aritii/service-client`).
- **Code Quality:** Automated linting, syntax verification, and environment example parity checks.

### 2. Continuous Deployment (CD) — `.github/workflows/deploy.yml` & `cd.yml`
- **Change Detection:** Automatically filters and identifies precisely which service (`identity-service`, `commerce-service`, `delivery-service`, or `gateway`) received changes.
- **Automated Deployment Orchestration:** Dispatches deployment triggers to [Render](https://render.com) web services upon successful CI test completion on `main`.
- **Zero-Downtime Rolling Deploys:** Ensures continuous availability of public APIs and customer traffic.
- **Automated Health Checks:** Post-deployment status verification against service health endpoints before completing the deployment cycle.

---

## 🛠️ Technology Stack Summary

- **Frontend Applications:**
  - **Framework:** React 18, Vite
  - **Languages:** JavaScript (ES6+), TypeScript
  - **Styling & Components:** Tailwind CSS, Lucide React
  - **Maps & Logistics:** Leaflet, OpenStreetMap
- **Backend & APIs:**
  - **Runtime & Framework:** Node.js, Express
  - **Architecture:** Microservices coordinated via Central API Gateway
  - **Security:** JWT (Access & Refresh tokens), PKCE flow, bcrypt hashing, service-to-service internal credentials
- **Databases & Storage:**
  - **Relational DB:** PostgreSQL (Identity Service)
  - **Document DB:** MongoDB (Commerce Service, Delivery Service)
  - **Cache & Rate Limiting:** Redis
  - **Media Storage:** Cloudinary
- **DevOps & Cloud Infrastructure:**
  - **CI/CD:** GitHub Actions (Automated testing, linting, and multi-service deploy pipelines)
  - **Backend Hosting:** [Render](https://render.com)
  - **Frontend Hosting:** [Vercel](https://vercel.com)

---

## 👥 Team Members

- **Yihune Belay**
- **Nedhi Jemal**

---

## 📋 Submission Notes

This repository acts as the central hub and evaluation index for the **Ariiti Market** platform submission. Source code repositories remain decoupled to preserve independent build, containerization, and continuous deployment pipelines.

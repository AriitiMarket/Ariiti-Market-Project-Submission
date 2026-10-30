# Ariiti Market — Project Submission

**Project Name:** Ariiti Market  
**Description:** A local-first Ethiopian e-commerce marketplace, merchant operations, and delivery logistics platform.

---

## Project Overview

Ariiti Market connects buyers, local sellers, delivery providers, and platform administrators into a unified digital commerce platform. Designed to address local market logistics and business workflows, the system provides multi-vendor commerce, verified merchant onboarding, dynamic location and route logistics, and end-to-end order tracking.

---

## Project Demonstration



---

## Source Code Repositories

The project codebase is organized across three specialized repositories:

| Repository | GitHub Link | Description |
| :--- | :--- | :--- |
| **Backend Microservices** | [AriitiMarket/backend-micro](https://github.com/AriitiMarket/backend-micro) | Node.js microservices (`identity-service`, `commerce-service`, `delivery-service`), API Gateway, polyglot persistence (PostgreSQL + MongoDB), and automated GitHub Actions CI/CD pipelines. |
| **Marketplace Web Frontend** | [AriitiMarket/aritii-seller-buyer-web](https://github.com/AriitiMarket/aritii-seller-buyer-web) | Customer storefront and Seller Center portal (product catalog, dynamic search, cart and checkout, escrow payments, order management). |
| **Admin & Operations Console** | [AriitiMarket/Aritii-admin-web](https://github.com/AriitiMarket/Aritii-admin-web) | Dedicated management portal for Super Admins and Operations Admins (order monitoring, merchant verification, SLA tracking, disputes). |

---

## System Architecture & Polyglot Database Design

Ariiti Market uses a polyglot persistence model, pairing each domain service with the database engine best suited to its requirements:

```text
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

## Database Strategy & Service Breakdown

### 1. Identity Service — PostgreSQL
- **Engine:** PostgreSQL (`pg` connection pool)
- **Role:** Central authentication, user accounts, and Role-Based Access Control (RBAC).
- **Design Rationale:**
  - Enforces relational integrity, ACID compliance, and foreign key constraints between `users`, `admin_roles`, and `admin_user_roles`.
  - Guarantees strict transactional security for password hashing (bcrypt), verification statuses, and fine-grained administrative scoping.

### 2. Commerce Service — MongoDB
- **Engine:** MongoDB with Mongoose ODM
- **Role:** Businesses, multi-shop management, dynamic product catalog, inventory, multi-item shopping carts, wishlists, and escrow orders.
- **Design Rationale:**
  - Handles dynamic, nested data structures where products have varied variants, attributes, media, and specifications.
  - Provides fast read and write performance under heavy browsing and checkout traffic.

### 3. Delivery & Logistics Service — MongoDB
- **Engine:** MongoDB with Mongoose ODM & GeoJSON support
- **Role:** Delivery location hierarchies, ports, dynamic delivery zones, provider assignment, delivery requests, and live package tracking.
- **Design Rationale:**
  - Provides native geospatial indexing (`2dsphere`) and GeoJSON polygons/coordinates for location mapping and route calculation.
  - Allows logistics milestones, dispatch events, and provider status tracking to evolve without complex schema migrations.

---

## DevOps: Continuous Integration & Continuous Deployment (CI/CD)

The backend microservices repository includes an automated CI/CD pipeline built on GitHub Actions and Render deploy hooks:

### 1. Continuous Integration (CI) — `.github/workflows/ci.yml`
- **Automated Triggering:** Runs on pushes and pull requests across `main` and active development branches.
- **Automated Test Suites:** Executes unit and integration tests across Node.js 20 runtime environments for `identity-service`, `commerce-service`, and `delivery-service`.
- **Shared Packages & Architecture Validation:** Verifies dependency consistency and architectural boundaries across internal shared packages (`@aritii/authz`, `@aritii/database`, `@aritii/internal-auth`, `@aritii/service-client`).
- **Code Quality:** Automated linting, syntax verification, and environment example checks.

### 2. Continuous Deployment (CD) — `.github/workflows/deploy.yml` & `cd.yml`
- **Path-Based Change Detection:** Identifies which microservice (`identity-service`, `commerce-service`, `delivery-service`, or `gateway`) was updated.
- **Automated Deployment:** Dispatches deployment triggers to Render web services once CI passes on `main`.
- **Zero-Downtime Rolling Deploys:** Maintains continuous service availability for client traffic.
- **Automated Health Checks:** Runs post-deployment status probes against service health endpoints before completing the release.

---

## Technology Stack Summary

- **Frontend Applications:**
  - Framework: React 18, Vite
  - Languages: JavaScript (ES6+), TypeScript
  - Styling & Components: Tailwind CSS, Lucide React
  - Maps & Logistics: Leaflet, OpenStreetMap
- **Backend & APIs:**
  - Runtime & Framework: Node.js, Express
  - Architecture: Microservices coordinated via Central API Gateway
  - Security: OAuth 2.1 / OIDC code exchange, JWT (Access & Refresh tokens), PKCE (S256), bcrypt hashing, service-to-service internal credentials
- **Databases & Storage:**
  - Relational Database: PostgreSQL (Identity Service)
  - Document Database: MongoDB (Commerce Service, Delivery Service)
  - Cache & Rate Limiting: Redis
  - Media Storage: Cloudinary
- **DevOps, Containerization & Cloud Infrastructure:**
  - Containerization: Multi-stage Docker & Docker Compose (isolated bridge network, automated health checks, persistent volumes)
  - CI/CD: GitHub Actions (automated testing, linting, and multi-service deploy pipelines)
  - Backend Hosting: Render
  - Frontend Hosting: Vercel

---

## Team Members

- **Yihune Belay**
- **Nedhi Jemal**

---

## Submission Notes

This repository acts as the central hub and evaluation index for the Ariiti Market platform submission. Source code repositories remain decoupled to preserve independent build, containerization, and continuous deployment pipelines.

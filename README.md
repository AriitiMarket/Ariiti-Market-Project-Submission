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
| **Backend Microservices** | [AriitiMarket/backend-micro](https://github.com/AriitiMarket/backend-micro) | Node.js microservices (`identity-service`, `commerce-service`, `delivery-service`), API Gateway, JWT/PKCE authentication, and PostgreSQL databases. |
| **Marketplace Web Frontend** | [AriitiMarket/aritii-seller-buyer-web](https://github.com/AriitiMarket/aritii-seller-buyer-web) | Customer storefront and Seller Center portal (product catalog, dynamic search, cart & checkout, escrow payments, order management). |
| **Admin & Operations Console** | [AriitiMarket/Aritii-admin-web](https://github.com/AriitiMarket/Aritii-admin-web) | Dedicated management portal for Super Admins and Operations Admins (order monitoring, merchant verification, SLA tracking, disputes). |

---

## 🏗️ System Architecture

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
                      ▼                         ▼                         ▼
          ┌────────────────────────────────────────────────────────────────────────┐
          │                         PostgreSQL & Redis DBs                         │
          └────────────────────────────────────────────────────────────────────────┘
```

---

## 🛠️ Technology Stack

- **Frontend Applications:**
  - **Framework:** React 18, Vite
  - **Language:** JavaScript & TypeScript
  - **Styling:** Tailwind CSS, Lucide React
  - **Maps & Geo:** Leaflet, OpenStreetMap
- **Backend & APIs:**
  - **Runtime & Framework:** Node.js, Express
  - **Architecture:** Microservices with reverse-proxy API Gateway
  - **Security & RBAC:** JWT, PKCE flow, bcrypt password hashing, scoped admin permissions
- **Databases & Cache:**
  - **Database:** PostgreSQL (Relational persistence)
  - **Caching & Rate Limiting:** Redis
- **Cloud Infrastructure & Hosting:**
  - **Backend Services:** [Render](https://render.com)
  - **Web Applications:** [Vercel](https://vercel.com)

---

## 👥 Team Members

- **Yihune Belay**
- **Nedhi Jemal**

---

## 📋 Submission Notes

This repository acts as the central hub and evaluation index for the **Ariiti Market** platform submission. Source code repositories remain decoupled to preserve independent build, containerization, and continuous deployment pipelines.

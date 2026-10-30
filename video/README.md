# Ariiti Market — Demonstration Videos & Screencasts

This directory documents the project demonstrations, system walkthroughs, and architecture presentations for **Ariiti Market**.

---

## 📺 Demonstration Video Links

| Demo Type | Platform | Link | Duration | Description |
| :--- | :--- | :--- | :--- | :--- |
| **Full Platform Walkthrough** | YouTube / Drive | `[INSERT VIDEO LINK HERE]` | ~10-15 min | End-to-end demonstration covering Buyer, Seller, Delivery Provider, and Admin workflows. |
| **Buyer Storefront & Checkout** | YouTube / Drive | `[INSERT VIDEO LINK HERE]` | ~3-5 min | Product discovery, filtering, cart, dynamic delivery quote, and checkout flow. |
| **Seller Central & Shop Operations** | YouTube / Drive | `[INSERT VIDEO LINK HERE]` | ~3-5 min | Merchant onboarding, catalog management, inventory tracking, and order fulfillment. |
| **Delivery Provider Portal** | YouTube / Drive | `[INSERT VIDEO LINK HERE]` | ~3-5 min | Available batch dispatch, live route status, driver availability, and wallet payouts. |
| **Admin & Operations Console** | YouTube / Drive | `[INSERT VIDEO LINK HERE]` | ~3-5 min | Super Admin & Operations Admin RBAC, platform settings, disputes, and delivery zone configuration. |

> [!TIP]
> **Video Sharing Guidelines:**
> - **YouTube:** Recommended setting: **Unlisted** (anyone with the URL can view without searching).
> - **Google Drive:** Ensure access permissions are set to **"Anyone with the link can view"**.
> - **Loom / Vimeo:** Provide direct public or unlisted sharing links with playback controls enabled.

---

## 📑 Video Walkthrough Outline

### 1. Introduction & Architecture (0:00 - 2:00)
- Platform problem statement and Ethiopian local-first commerce context.
- High-level architecture: API Gateway edge, microservices (Identity, Commerce, Delivery).
- Polyglot persistence overview: PostgreSQL (Users, RBAC, Relational integrity) + MongoDB (Products, Orders, GeoJSON Zones).

### 2. Buyer Experience (2:00 - 5:00)
- Storefront navigation, category browsing, full-text product search.
- Location-based zone selection and dynamic delivery fee estimation.
- Cart synchronization, checkout flow, and live order tracking.

### 3. Seller Operations & Storefront (5:00 - 8:00)
- Seller registration and shop setup wizard.
- Product catalog creation (variants, attributes, media uploads).
- Incoming orders, inventory reservation, and dispatch fulfillment status.

### 4. Delivery Partner & Fleet Dispatch (8:00 - 11:00)
- Delivery partner sign-in and workspace navigation (`/provider`).
- Viewing available deliveries, accepting batches, and route progress updates.
- In-app driver wallet balance and payout requests.

### 5. Platform Admin & Operations Management (11:00 - 14:00)
- Super Admin vs. Operations Admin role separation and granular permissions.
- Merchant approval, delivery zone and route management.
- Platform audit trails, metrics, and dispute resolution.

---

## 💾 Local Video Files Note
For Git repository storage, video files exceeding 50 MB should be hosted on external streaming platforms (YouTube, Google Drive, or Vimeo) to maintain repository cloning speed and adhere to GitHub file size constraints.

# My House — Product Requirements Document

**Version:** 1.1  
**Date:** 2026-06-08  
**Status:** Draft

---

## 1. Overview

**My House** is a mobile and web application that helps homeowners document, track, and remember everything about their home — from paint colors and flooring to maintenance history and product receipts. When a home changes hands, the new owner receives a complete, organized record of the home's history.

### Problem Statement

Homeowners frequently lose track of specific materials, products, and service history tied to their home. Without this information:
- Patching paint or matching flooring requires guesswork or full replacement.
- Maintenance tasks (filter changes, system servicing) go undocumented and undated.
- Future owners inherit a home with no historical context.
- Renovation projects stall because original product sources are unknown.

### Goals

- Give homeowners a single place to document all materials, finishes, and products in their home.
- Provide a maintenance log with dates, service providers, costs, and product details.
- Allow the full record to be transferred to future homeowners.
- Make it easy to look up product details for patching, matching, or reordering.

### Target Users

Anyone who owns a home — first-time homeowners, long-term owners preparing to sell, and buyers receiving documentation from a seller.

### Monetization

Free — no charge to users. No paid tiers planned for v1.

### MVP Scope

The minimum viable product is **Rooms & Finishes** only. This is the core problem: homeowners losing track of paint colors, flooring, and materials. All other features (maintenance log, reminders, sharing) are post-MVP.

---

## 2. Core Features

### 2.1 Rooms & Finishes

Users can create a room-by-room inventory of their home. Each room can store:

- **Room name and type** (e.g., "Primary Bedroom," "Kitchen," "Basement")
- **Paint** — brand, product name, color name, color code (hex or brand code), finish (matte, eggshell, satin, etc.), base type, where purchased
- **Flooring** — material type (hardwood, LVP, tile, carpet, etc.), brand, product name/SKU, color, where purchased, direct product URL, in-stock status
- **Other finishes** — trim, ceiling paint, cabinetry finish, tile grout color, etc.
- **Notes** — free-text notes per room (e.g., "second coat applied 6 months after first")
- **Photos** — ability to attach photos of the room or specific materials

#### Product Linking (Finishes)

Each finish entry supports a **direct product link** — a URL pointing to the exact product on the retailer's website (e.g., a specific SKU on Floor & Decor, Home Depot, Wayfair, etc.). This link is displayed prominently in the UI as a tappable "Buy Again" button so the user can reorder in one tap without searching.

Each linked finish also has an **in-stock status** field, manually set by the user:
- `In Stock` — product is currently available at the linked URL
- `Discontinued / Out of Stock` — product is no longer available; user should note a substitute if found
- `Unknown` — default state; user hasn't checked

The status is a manual flag (v1). Users are responsible for updating it when they check the retailer site. Automated stock checking is out of scope for v1.

This applies to all finish types, not just flooring — paint, tile, trim, and any other material where future reordering or matching is needed.

### 2.2 Accessories & Purchases

Users can log purchased items associated with a room or the home generally:

- Item name and description
- Brand and model/SKU
- Purchase date
- Retailer and purchase link
- Price paid
- Room or area it belongs to
- Photos or receipt attachments
- Notes (e.g., "matches the trim in the hallway")

This is useful for furniture, fixtures, hardware, and any item a future owner might want to source or replace.

### 2.3 Maintenance Log

A chronological record of maintenance events for the home. Each entry includes:

- **Date performed**
- **Category** (e.g., Plumbing, HVAC, Electrical, Roof, Well, Septic, Appliance, General)
- **Description** of the work done
- **Service provider** — company name, contact info
- **Cost**
- **Product used** — brand, model, part number (e.g., filter brand and size)
- **Where to buy** — retailer or product link for consumables
- **Next service date** (optional, triggers a reminder)
- **Notes and attachments** (receipts, invoices, photos)

Example entries:
- Water filter swap: date, filter brand/model, retailer link
- Routine water system maintenance: date, provider, cost
- Septic system pump: date, provider, cost
- Roof inspection or replacement: date, material type, age
- Well service: date, pump type/model, provider

### 2.4 Reminders

Users can set reminders tied to maintenance intervals:

- Linked to a maintenance log entry (e.g., "remind me 6 months after last filter change")
- Or standalone (e.g., "check gutters every fall")
- Push notification (mobile) and/or email reminder
- Ability to snooze or mark complete, which logs a new maintenance entry

### 2.5 Home Details

A top-level profile for the home storing general information:

- Address
- Year built
- Square footage
- Lot size
- Home type (single family, condo, townhouse, etc.)
- Key systems inventory: roof age and material, well age and pump type, HVAC system(s), water heater, septic vs. sewer
- Utility providers (electric, gas, water, trash, internet)
- HOA details (if applicable)
- Notes

### 2.6 Sharing & Transfer

- Homeowners can share their home record with other users (e.g., a spouse or co-owner) with full read/write access.
- When selling, the owner can generate a shareable link or transfer ownership to a new owner.
- The new owner receives the complete history: rooms, finishes, accessories, and maintenance log.
- A read-only "buyer preview" mode allows sharing before transfer is finalized.

---

## 3. User Stories

### Rooms & Finishes

- As a homeowner, I want to log the exact paint color and brand for each room so I can buy the correct paint if I need to patch a wall.
- As a homeowner, I want to record my flooring product and SKU so I can order matching replacement planks in the future.
- As a homeowner, I want a direct "Buy Again" link for any finish so I can reorder the exact product without searching for it.
- As a homeowner, I want to mark a finish as in stock, out of stock, or unknown so I know at a glance whether I can still buy it.
- As a homeowner, I want to attach photos to a room entry so I have a visual reference alongside the product details.

### Accessories & Purchases

- As a homeowner, I want to log where I bought a light fixture and how much I paid so I can find a matching one if it breaks.
- As a homeowner, I want to store receipt images with a purchase so I have proof of purchase for warranty claims.

### Maintenance Log

- As a homeowner, I want to record every maintenance event with the date, provider, and cost so I have a complete service history.
- As a homeowner, I want to store the specific water filter model I use so I can easily reorder it.
- As a homeowner, I want to see when my roof was last inspected or replaced and what material was used.
- As a homeowner, I want to know my well pump type and age so I can provide that information to a service technician.

### Reminders

- As a homeowner, I want to be reminded when my water filter is due for replacement so I don't forget.
- As a homeowner, I want recurring reminders for seasonal tasks (e.g., gutter cleaning, HVAC filter changes).

### Sharing & Transfer

- As a homeowner, I want to share my home record with my partner so we both have access to the same information.
- As a seller, I want to transfer my home's complete record to the buyer so they know the full history.
- As a buyer, I want to receive the previous owner's maintenance history so I know what has been done and when.

---

## 4. Data Entities

### Home
- `id`, `address`, `year_built`, `sqft`, `lot_size`, `home_type`
- `roof_material`, `roof_age`, `well_age`, `well_pump_type`
- `hvac_details`, `water_heater_details`, `septic_or_sewer`
- `utility_providers` (array), `hoa_details`, `notes`
- `owner_id`, `created_at`, `updated_at`

### Room
- `id`, `home_id`, `name`, `type`, `notes`, `photos` (array)
- `created_at`, `updated_at`

### Finish
- `id`, `room_id`, `finish_type` (paint | flooring | trim | ceiling | tile | other)
- `brand`, `product_name`, `sku`, `color_name`, `color_code`, `finish_level`
- `retailer` (store name), `product_url` (direct link to the exact product listing)
- `in_stock_status` (in_stock | out_of_stock | unknown — default: unknown)
- `notes`, `photos`

### Accessory
- `id`, `home_id`, `room_id` (optional), `name`, `description`
- `brand`, `model`, `sku`, `purchase_date`, `retailer`, `purchase_url`, `price`
- `notes`, `attachments` (receipts, photos)

### MaintenanceRecord
- `id`, `home_id`, `date`, `category`, `description`
- `provider_name`, `provider_contact`, `cost`
- `product_brand`, `product_model`, `product_sku`, `product_url`
- `next_service_date`, `notes`, `attachments`

### Reminder
- `id`, `home_id`, `maintenance_record_id` (optional), `title`
- `due_date`, `recurrence_interval`, `notification_method` (push | email | both)
- `status` (pending | snoozed | completed)

### User
- `id`, `name`, `email`, `notification_preferences`

### HomeAccess
- `id`, `home_id`, `user_id`, `role` (owner | editor | viewer)
- `invited_at`, `accepted_at`

---

## 5. Key Decisions

| Decision | Choice | Rationale |
|---|---|---|
| Platform | Mobile + Web | Homeowners need access on-the-go and from a desktop |
| Monetization | Free | No paid tiers in v1 |
| MVP | Rooms & Finishes | Core problem; validates the app before building out maintenance/reminders |
| Offline support | Required | Core features must work without internet (spotty connectivity, on-site use) |
| Sharing model | Role-based access (owner / editor / viewer) | Supports co-owners, contractors, and buyer previews |
| Transfer model | Ownership transfer to new owner | Ensures full history follows the home, not just the original user |
| Photo/attachment storage | Per-room, per-finish, per-maintenance-record | Keeps context co-located with the data it documents; storage cap TBD |
| Reminder delivery | Push + email | Covers both mobile-first and non-mobile users |
| In-stock tracking | Manual flag on finish records | Automating stock checks would require retailer API integrations; manual is simpler for v1 |
| Maintenance categories | Predefined list + custom | Structured enough to filter/search, flexible enough for any home type |
| Development approach | AI-assisted (Claude Code) | Solo builder with no prior dev experience; stack chosen for AI-codeability and simplicity |

---

## 6. Recommended Tech Stack

This stack is chosen for solo development with AI assistance (Claude Code), offline-first requirements, and cross-platform mobile + web support. No prior development experience is assumed.

### Frontend — Expo (React Native)

[Expo](https://expo.dev) is a framework built on top of React Native that lets you write one JavaScript/TypeScript codebase and deploy to iOS, Android, and web. It is the most AI-friendly mobile stack — Claude Code handles it well, the documentation is excellent, and you don't need to configure native build tools to get started.

- Language: **TypeScript**
- Navigation: **Expo Router** (file-based routing, works on mobile and web)
- UI components: **NativeWind** (Tailwind CSS syntax for React Native) or **Tamagui**

### Backend & Database — Supabase

[Supabase](https://supabase.com) is a hosted backend that provides a Postgres database, user authentication, file storage, and a real-time API — all with minimal configuration. It has a generous free tier and is well-supported by AI coding tools.

- **Database:** Postgres (structured, relational — fits the home/room/finish data model well)
- **Auth:** Supabase Auth (email/password + magic link out of the box)
- **File storage:** Supabase Storage (photos, receipts, attachments)
- **Offline sync:** WatermelonDB or MMKV for local-first caching, synced to Supabase

### Offline Strategy

Use **WatermelonDB** (a local SQLite database for React Native) as the primary data store on-device, with Supabase as the sync target. This means the app works fully offline and syncs when connectivity is available.

### Summary

| Layer | Technology |
|---|---|
| Mobile + Web UI | Expo (React Native) |
| Language | TypeScript |
| Navigation | Expo Router |
| Backend / API | Supabase |
| Database (cloud) | Supabase Postgres |
| Auth | Supabase Auth |
| File storage | Supabase Storage |
| Offline / local DB | WatermelonDB |
| Deployment | Expo EAS (mobile) + Vercel or Netlify (web) |

---

## 7. Out of Scope (v1)

- Automated retailer stock checking (e.g., live Home Depot inventory lookup)
- Financial/budgeting features beyond recording what was spent
- Contractor marketplace or service booking
- Integration with smart home devices
- AI-generated maintenance schedules (could be a v2 feature)

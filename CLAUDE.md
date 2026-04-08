# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

**Iatris** is a web-based dispatch platform connecting patients in underserved communities to nearby **Community Health Workers (CHWs)**. Think Uber for basic healthcare: patient submits a request → system triages urgency and matches nearest available CHW → CHW accepts and visits → outcome logged for NGO analytics.

Three user roles: **Patient** (submits health requests), **CHW** (receives/accepts dispatches, logs outcomes), **Admin/NGO** (analytics, CHW management).

## Planned Tech Stack (Phase 1 MVP)

| Layer | Choice |
|---|---|
| Frontend | React + TypeScript |
| Styling | Tailwind CSS |
| Maps | Leaflet + OpenStreetMap (100% Free) |
| Backend | Next.js API Routes (full-stack JS) |
| Database + Auth | Supabase (Postgres, Realtime, Row-Level Security, Auth) |
| Real-time | Supabase Realtime |
| Geolocation matching | Browser Geolocation API + Turf.js |
| Hosting | Vercel |

## Core Domain Logic

**Smart Matching:** When a request comes in, find the nearest available CHW using Turf.js for spatial calculations, filtered by skill tags matching the symptom category and availability status.

**Symptom Categories:** maternal, wound care, child illness, mental health, medication, general.

**Urgency Levels:** low / medium / high.

**Visit Lifecycle:** `pending` → `accepted` (CHW claims it) → `in_progress` → `completed` (CHW logs outcome: actions taken, referral needed, follow-up needed).

## Architecture Decisions

- **Supabase Realtime** drives live map updates and request notifications — CHWs should see new requests without polling.
- **Row-Level Security (RLS)** in Supabase handles role-based data access — patients see only their own requests, CHWs see requests in their area, admins see everything.
- **Magic link auth** preferred over passwords for the patient/CHW flow (low-tech literacy users).
- **Mobile-first, low-bandwidth:** Keep bundle size minimal; avoid heavy assets. CHWs use this in the field on mobile browsers.

## Phase Roadmap

- **Phase 1 (MVP):** Core request/dispatch/log loop, live map, admin analytics dashboard.
- **Phase 2:** SMS/USSD fallback (Twilio or Africa's Talking), AI symptom triage (Anthropic Claude API), offline mode (Workbox service workers), i18n (i18next), CHW certification tracking.
- **Phase 3:** Multi-tenant GNEC network (1,600 subsidiaries), predictive demand ML (Python/scikit-learn), FHIR-compliant records, React Native apps, supply chain module.

## Specs

Detailed requirements live in `spec/`:
- `spec/01_overview.md` — problem statement, user types, product purpose
- `spec/02_phase1_mvp.md` — MVP features, product and engineering requirements
- `spec/03_phase2_enhancement.md` — SMS fallback, AI triage, offline mode, i18n
- `spec/04_phase3_scale.md` — enterprise multi-tenancy, FHIR, ML, native apps

## Development Workflow & Tooling

- **Supabase MCP:** You must use the Supabase MCP to manage database operations, pull remote schemas, and fetch necessary environment variables. Rely on the MCP to populate `.env` files automatically connecting to the user's Supabase project rather than requesting manual key generation.

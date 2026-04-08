# 2. Phase 1 — MVP (Hackathon Build)

This outlines the minimum viable product (MVP) to be demonstrated in a 2-5 minute pitch video.

## Core Features

1. **Patient Request Flow**
   - Patients fill out a form with:
     - Name
     - Location (auto-detected via browser geolocation or manual entry)
     - Symptom category (dropdown: maternal, wound care, child illness, mental health, medication, general)
     - Urgency level (low/medium/high)
     - Optional notes

2. **CHW Dashboard**
   - CHWs view incoming requests on a map.
   - CHWs can easily accept or decline requests.
   - CHWs can view patient details and get directions to the patient.

3. **Smart Matching**
   - The system automatically matches patient requests to the nearest available CHW.
   - Matching factors: location proximity, specific skill tags, and availability status.

4. **Live Map View**
   - A real-time map displaying:
     - Patient locations
     - Nearby CHWs (available and unavailable)
     - Active dispatches

5. **Visit Logging**
   - After completing a visit, the CHW logs a basic outcome detailing:
     - What was done
     - Referral needed? (yes/no)
     - Follow-up needed? (yes/no)

6. **Admin Dashboard**
   - Provides a simple analytics view for NGO admins, including:
     - Total requests over time
     - Average response times
     - Heat map of health demand
     - CHW utilization metrics

## Product Requirements

- **Responsive Web App:** Must work perfectly on mobile browsers (critical for CHWs out in the field).
- **Real-Time Updates:** Requests must appear in front of the CHW immediately without needing to refresh.
- **Geolocation Matching:** The core loop relies on spatial distance calculations.
- **Role-Based Access:** Defined user states for Patient, CHW, and Admin.
- **Low Bandwidth Optimization:** Must remain lightweight with minimal assets to accommodate poor internet connectivity.

## Engineering Requirements & Tech Stack

| Layer | Choice | Why |
| :--- | :--- | :--- |
| **Frontend** | React + TypeScript | Fast dev cycle, reusable UI components, aligns with team knowledge. |
| **Styling** | Tailwind CSS | Rapid prototyping, responsive out of the box. |
| **Maps** | Mapbox GL JS or Leaflet + OpenStreetMap | Generous free tiers, supports offline-ish scenarios, better suited for rural/humanitarian use cases than Google Maps. |
| **Backend** | Node.js + Express or Next.js API Routes | Keeps it straightforward using full-stack JavaScript. |
| **Database** | Supabase (Postgres + Realtime) | Free tier, integrated Auth, row-level security, built-in real-time subscriptions for live updates. |
| **Real-time** | Supabase Realtime or Socket.io | Allows for live dispatch updates without long-polling. |
| **Geolocation** | Browser Geolocation API + Turf.js | Turf.js allows complex distance calculations and nearest-neighbor matching directly in JS. |
| **Auth** | Supabase Auth | Handles role-based routing; supports magic links (passwordless flow is great for low-tech literacy areas). |
| **Hosting** | Vercel | Free, instant deployment, built specifically for Next.js/React. |

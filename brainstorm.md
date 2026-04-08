1. PROJECT OVERVIEW
What are you trying to do?
Build a web-based dispatch platform that connects people in underserved communities to nearby Community Health Workers (CHWs) for basic healthcare services — think symptom triage, medication delivery, wound care, prenatal checkups, health education. Essentially Uber meets healthcare for areas where clinics are too far, too expensive, or too overwhelmed.
Who is this for?
Two user types:

Patients/Requesters — people in rural or underserved areas who need basic health services but can't easily access a clinic. Could be a pregnant woman needing a prenatal check, an elderly person needing wound care, a parent with a sick child.
Community Health Workers (CHWs) — trained volunteers or paid workers already embedded in communities (WHO estimates 5+ million globally). They need a system to receive requests, manage their schedule, and log visits.

Secondary users: NGO Administrators at GNEC subsidiaries who oversee CHW networks, track health trends, and allocate resources.
What problems does this solve?

400+ million people globally lack access to essential health services
CHWs exist but are dispatched inefficiently — often paper-based, phone-call-based, or walk-in only
No centralized data on community health needs, so NGOs can't allocate resources effectively
Patients don't know which CHWs are available, nearby, or qualified for their issue

What does the product do?
A patient submits a health request (symptoms, urgency, location). The system triages urgency, finds the nearest available CHW with the right skills, dispatches them, and tracks the visit from request to completion. After the visit, data is logged for the NGO to use for resource planning.

2. PHASES
PHASE 1 — MVP (Hackathon Build)
This is what you demo in your 2-5 minute video.
Core Features:

Patient Request Flow — patient fills out a form: name, location (auto-detect via browser geolocation or manual entry), symptom category (dropdown: maternal, wound care, child illness, mental health, medication, general), urgency level (low/medium/high), optional notes
CHW Dashboard — CHWs see incoming requests on a map, can accept/decline, see patient details and directions
Smart Matching — system matches request to nearest available CHW based on location proximity, skill tags, and availability status
Live Map View — real-time map showing patient location, nearby CHWs, and active dispatches
Visit Logging — after a visit, CHW logs basic outcome: what was done, referral needed (yes/no), follow-up needed (yes/no)
Admin Dashboard — simple analytics view for NGO admins: total requests, response times, heat map of demand, CHW utilization

Product Requirements (Phase 1):

Responsive web app (works on mobile browsers — critical for CHWs in the field)
Real-time updates (request comes in, CHW sees it immediately)
Geolocation-based matching
Role-based access: Patient, CHW, Admin
Works on low bandwidth (lightweight, minimal assets)

Engineering Requirements & Tech Stack (Phase 1):
LayerChoiceWhyFrontendReact + TypeScriptFast dev, component reuse, your team knows itStylingTailwind CSSRapid prototyping, responsive out of the boxMapsMapbox GL JS or Leaflet + OpenStreetMapFree tier is generous, works offline-ish, better than Google Maps for humanitarian use casesBackendNode.js + Express or Next.js API routesKeep it simple, full-stack JSDatabaseSupabase (Postgres + Realtime)Free tier, built-in auth, real-time subscriptions for live updates, row-level securityReal-timeSupabase Realtime or Socket.ioLive dispatch updates without pollingGeolocationBrowser Geolocation API + Turf.jsTurf.js for distance calculations and nearest-neighbor matchingAuthSupabase AuthRole-based, supports magic link (no password needed — great for low-tech users)HostingVercelFree, instant deploys, works with Next.js natively

PHASE 2 — Post-Hackathon Enhancement
Features:

SMS/USSD Fallback — patients without smartphones can text in a request via Twilio or Africa's Talking API
AI Symptom Triage — use an LLM (Claude API) to ask follow-up questions and better assess urgency before dispatching
Offline Mode — service worker + local cache so CHWs can log visits without connectivity and sync later
Multi-language Support — i18n for local languages
CHW Certification Tracking — track training, certifications, and skill tags per CHW

Additional Tech:

Twilio API for SMS
Anthropic Claude API for symptom triage
Workbox for offline/PWA support
i18next for localization


PHASE 3 — Scale
Features:

GNEC Network Integration — each of the 1,600 subsidiaries gets their own admin portal, shared data layer for cross-org insights
Predictive Demand Mapping — ML model trained on historical request data to predict where demand will spike (seasonal illness, outbreaks)
Supply Chain Module — track medical supply inventory per CHW and auto-request restocks
Interoperability — FHIR-compliant health records so data can plug into national health systems
Mobile Native Apps — React Native for iOS/Android

Additional Tech:

FHIR API standards
React Native
ML pipeline (Python, scikit-learn or similar)
Multi-tenant architecture
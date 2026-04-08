# 3. Phase 2 — Post-Hackathon Enhancement

This phase builds upon the MVP by adding features to support more rugged environments, handle edge cases, and utilize AI for deeper triage.

## Enhancements & Features

1. **SMS/USSD Fallback**
   - Patients without smartphones or reliable internet can text a shortcode to submit a request. The system parses the SMS into a structured request for the CHW dashboard.

2. **AI Symptom Triage**
   - Integrates an advanced LLM to ask automated follow-up questions to the patient.
   - Purpose: Better assess urgency and filter noise *before* a CHW is officially dispatched.

3. **Offline Mode**
   - Implements a service worker and local browser caching.
   - CHWs can log visit data while completely disconnected from a network, which then automatically syncs back to the server once connectivity is restored.

4. **Multi-language Support (i18n)**
   - Translates the Patient side and CHW Dashboard into essential local languages to support diverse demographics.

5. **CHW Certification Tracking**
   - An internal tracking feature letting admins log each CHW's specialized training, active certifications, and skill tags. Ensure dispatches for specific issues (e.g., prenatal care) only route to certified workers.

## Additional Tech Stack Elements

- **Twilio API (or Africa's Talking API):** Used for two-way SMS parsing and USSD session support.
- **Anthropic Claude API:** Drives the conversational symptom triage logic to process and structure symptoms safely.
- **Workbox:** Generates and manages the service workers handling the offline/PWA caching layer.
- **i18next:** The industry-standard library to handle dynamic localization and language switching.

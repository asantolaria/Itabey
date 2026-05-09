# Itabey / Asha — Product Requirements Document

**Revision:** 2
**Revision date:** 2026-05-08
**Author:** Alex Santolaria (technical consultant)
**Status:** Draft — for vendor evaluation
**Source document:** `docs/fuentes/Documento de Requerimientos Funcionales_ Itabey _ Asha.md` (Itabey CEO, v1.0)
**Spanish canonical version:** `docs/design/prd.md`
**Changes since Rev 1:** CEO feedback integrated in two rounds:
- *Round 1 (tactical):* explicit phasing matrix (§ 1.4); separation of internal calendar (FR-303) from bidirectional sync with external calendars showing cycle phase (FR-106); B2C + B2B account management with single persistent account and lossless migration (FR-1301–1304); in-product explanatory video (FR-702); professional patient-management profile as Phase 3 architectural preparation (FR-1305); explicit HL7/FHIR readiness (NFR-M09, E15); post-launch support and maintenance promoted to its own NFR section (§ 4.10).
- *Round 2 (strategic):* modular **depth tier model** elevated to a first-class architectural commitment (§ 1.5, FR-1306, FR-1307); functional modularity as NFR (NFR-SC06–07); dynamic feature activation as a vendor evaluation criterion (§ 12); reformulation of open question Q6 to align with the CEO's modularity thesis.

> This PRD reformulates the CEO's functional requirements document into a PRD structure to serve as the basis for evaluating development vendor proposals. Values marked 🏷️ **PROPOSAL** are technical inferences pending CEO validation. Decisions marked 🛡️ **NON-NEGOTIABLE** derive directly from the source document and cannot be negotiated without CEO authorisation.

---

## 1. Product vision and goals

### 1.1 Vision

Itabey is a digital system for **longitudinal women's health support**, focused on the recording, visualisation, interpretation, and follow-up of hormonal, physical, emotional, behavioural, and contextual data.

**Asha** is the conversational engine integrated into Itabey. It interprets data entered by the user, detects patterns, generates non-diagnostic hypotheses, offers contextual support, and recommends clinically validated educational content.

The product's core value **does not lie in data capture** but in its capacity for interpretation, learning, and continuous longitudinal support. The clinically validated, versioned knowledge base and the RAG engine running on top of it constitute the **defensible asset** of the product, alongside its user experience.

### 1.2 Goals

| ID | Goal | Measured via |
|----|------|--------------|
| G1 | Support the user in self-knowledge of her cyclical health through longitudinal data | D90 retention, registration frequency, NPS |
| G2 | Reduce friction in data entry through natural voice and wearable integration | % voice-driven entries, % users with connected wearable |
| G3 | Generate structured reports that facilitate medical consultations | % users who generate a report within 90 days, satisfaction of receiving professionals |
| G4 | Build a clinically validated, versioned biomedical knowledge base as the central asset | Volume of validated capsules, mean time to validation |
| G5 | Enable Asha as a decoupled, future-licensable engine via API/white-label | Public API coverage, third-party integration time |
| G6 | Comply with GDPR (Art. 9) and embed Privacy/Security by design from the architecture onward | Successful external audit, 0 data breach incidents |

### 1.3 Non-goals

| ID | Non-goal | Reason |
|----|----------|--------|
| NG1 | 🛡️ **Clinical diagnosis** | Asha does not diagnose, prescribe, or replace medical consultation (source § 3.3) |
| NG2 | CE marking / classification as a regulated medical device (MDR) in MVP | Out of scope for time and budget; architecture must allow it later |
| NG3 | HL7/FHIR compliance in MVP | Out of MVP. **It is required**, however, that the architecture allow later mapping without structural redesign — see § 4.10, NFR-M, E15 in § 12.2 |
| NG4 | Women's sports vertical in MVP | Deferred to Phase 2; architecture must reserve integration surface |
| NG5 | White-label / API licensing of Asha in MVP | Deferred; architecture must allow it from day 1 (source § 4.4) |
| NG6 | 🛡️ **Sale of personal data or commercial exploitation of individual information** | Ethical/GDPR commitment of the product |
| NG7 | Advanced wearables (Whoop, Oura beyond basic data) in MVP | Initial integrations: Apple Health + Google Health Connect |
| NG8 | Active scientific research with institutions in MVP | Architecture prepared, execution deferred |

### 1.4 Product phasing

> This section makes the product's temporal scope explicit. Each FR in § 3 keeps its MoSCoW priority (Must/Should/Could) — the priority indicates **what matters within its phase**; the phase indicates **when it ships**. The intent: that neither the internal team nor vendors mix levels when evaluating proposals.

| Phase | Horizon | Scope |
|-------|---------|-------|
| **Phase 1 — MVP** | Initial launch | Core functionality validating the value proposition: structured data capture, Asha conversation with RAG, internal calendar, main panel, basic reports, onboarding, full privacy and security, minimal dashboards, initial health integrations (Apple Health + Google Health Connect), risk detection and hard-stop |
| **Phase 2 — Near post-MVP** | 3–9 months post-launch | Moderated community, advanced self-knowledge panel, body map, shared panel (FR-305), full dashboards, bidirectional sync with external calendars (FR-106), reports for professionals (FR-402, FR-403), focus modules (FR-603), soft notifications (FR-801), full B2B account management (§ 3.13) |
| **Phase 3 — Future** | 12+ months | Women's sports vertical, professional patient-management profile (FR-1305), API licensing and white-label of Asha, advanced wearable integrations (Whoop, full Oura, Garmin), HL7/FHIR mapping, active scientific research with institutions |

#### 1.4.1 Summary by functional area

| Area | MVP (Phase 1) | Post-MVP (Phase 2) | Future (Phase 3) |
|------|---------------|--------------------|-------------------|
| Data capture | FR-101, FR-102, FR-104 (Apple Health + Google Health Connect), FR-105 | FR-103 (voice-only mode), FR-106 (bidirectional calendar sync) | FR-104 advanced wearables, HL7/FHIR mapping |
| Asha conversational | FR-201 to FR-209 | FR-210 (stable internal API) | Public API / white-label |
| Panels | FR-301, FR-303 | FR-302, FR-304, FR-305 | — |
| Calendar | FR-303 (internal) | FR-106 (bidirectional sync with external) | — |
| Reports | FR-401 | FR-402, FR-403 | — |
| Community and content | FR-502 (small initial catalogue) | FR-501, FR-503 (if podcast exists) | — |
| Personalisation | FR-601, FR-602 | FR-603 | — |
| Onboarding and help | FR-701, FR-702 (explanatory video) | — | — |
| Notifications | — | FR-801 | — |
| Privacy | FR-901 to FR-905 | — | — |
| Internal dashboards | FR-1001 (minimal), FR-1002 (partial) | FR-1001 (full), FR-1002 (full), FR-1003, FR-1004, FR-1005 | — |
| Integrations | FR-1101, FR-1103 (open architecture) | FR-1102 (full external calendars) | HL7/FHIR, integration with professional management profiles |
| Risk detection | FR-1201 | — | — |
| Account management | FR-1301 (single account), FR-1302 (free + individual), FR-1303 (free↔individual migration), FR-1306 (tiering capability, no prescriptive content), FR-1307 (basic feature flags) | FR-1302 (B2B), FR-1303 (B2B), FR-1304 (B2B privacy), FR-1306 (operational tiers) | FR-1305 (multi-user professional management profile) |

> **Proposal evaluation rule:** Vendor proposals must present **phases coherent with this table**. A proposal that mixes Phase 1 with Phase 2 without explicit distinction must be corrected before cost comparison.

### 1.5 Depth tier model and strategic modularity

> **First-class architectural commitment.** The system **must be born modular** — capable of supporting different levels of depth and access from day 1, even though externally it feels like a single coherent product. This section elevates functional modularity to the rank of Privacy by design and Security by design principles.

#### 1.5.1 Why this matters

Itabey operates in a hybrid B2C + B2B market with fundamentally different needs:

- **Corporate client (B2B):** buys **wellbeing, prevention, engagement** for employees. Requires a solid, easy-to-deploy tool with predictable operating cost. **Does not** need the full longitudinal introspective depth of the product.
- **Individual user (B2C):** seeks **deep self-knowledge, personalisation, longitudinal support, pattern analysis, contextual memory**. She is the *power user* with the highest LTV potential.

If the system delivers all advanced capabilities to B2B from the start, the risks are material: high-volume contracts at low prices against rising infrastructure/AI costs, *power users* with no natural upgrade path, eroded margins, loss of future pricing flexibility.

If the system **is born modular**, the organisation gains: a powerful corporate experience without runaway structural costs, B2B as a low-CAC mass acquisition channel, natural upgrade paths to premium tiers for individuals, higher LTV/margin per user, the ability to adapt plans and verticals without rebuilding the product.

#### 1.5.2 What this requires of the system

The PRD **does not prescribe** which features will go in which tier — that decision is deferred until real usage data is available. What is required is the **architectural capability** so that, when that decision is made, it is trivial to implement:

1. **Activation/deactivation of features by user, cohort, or tier** without code changes (feature flags as a first-class capability — FR-1307).
2. **Asha depth layers** parameterisable: long-term memory depth, number of detected patterns, insight frequency, type of personalisation available — all configurable per tier without redesign (FR-1306).
3. **Resource consumption tiers**: configurable quotas per tier on LLM calls, vector storage, inference tokens, voice processing. No tier consumes unlimited resources without a cap.
4. **Modular permissions** by feature and by person, not by monolithic role. A "B2B standard" tier user may have partial access to premium features if her organisation pays for them, without creating a new static role.
5. **Vertical adaptation** (sports, professional profile, etc.) as activation of modules over the common base, not as parallel branches of the product.

#### 1.5.3 What is not yet decided here

- Which exact features go in which tier (post-MVP decision, based on real usage signal).
- Commercial tier names (marketing decision).
- Tier pricing (commercial decision by the CEO).
- Which tier B2B client employees receive (per-contract decision).

> **Proposal evaluation rule:** A vendor proposal that delivers monolithic architecture with fixed-role permissions **does not meet** this PRD, even if it complies with every individual FR. Modular tiering capability is evaluated explicitly — see § 12.4.

---

## 2. Users and personas

### 2.1 Primary personas (end users)

#### P1 — **Lara**, the curious self-learner (28–40)

- **Role:** Urban professional woman, no diagnosed condition.
- **Technical level:** Intermediate. Daily wearable user, reads health and wellbeing podcasts.
- **Primary goal:** Understand her cycle and optimise wellbeing through self-knowledge.
- **JTBD:** *"Help me understand my body over time without having to see a doctor for every question."*
- **Preferred modes:** Real life, configurable.
- **Current frictions:** Fragmented apps (one for cycle, one for sleep, one for mood); none correlate; generic explanations.

#### P2 — **Mar**, the chronically symptomatic (30–50)

- **Role:** Woman living with a cyclical condition (endometriosis, PCOS, perimenopause, cyclical mental health).
- **Technical level:** Variable. High emotional load; intolerant of complex interfaces.
- **Primary goal:** Manage her condition and communicate better with her medical team.
- **JTBD:** *"Help me explain to my doctor what's happening with data, not feelings."*
- **Preferred modes:** Crisis (bad days), neurodivergent mode activatable.
- **Current frictions:** Difficulty articulating symptoms in consultation; sense of not being heard; gap between lived experience and clinical data.

#### P3 — **Sara**, the athlete (22–38)

- **Role:** Advanced or semi-professional sports practitioner.
- **Technical level:** Advanced. Intensive wearable user (Garmin, Apple Watch, Oura).
- **Primary goal:** Adjust training, recovery, and nutrition to her cycle phase.
- **JTBD:** *"Adjust my training to my cycle phase and tell me when to push and when to recover."*
- **Preferred modes:** Real life with data emphasis; direct or technical tone.
- **Current frictions:** Sports platforms ignore the cycle; literature is fragmented and unvalidated.

> **Note:** Sara consumes the MVP through habits, energy, and general correlations. The dedicated sports vertical (source § 23) is post-MVP.

### 2.2 Secondary persona

#### P4 — **Ana**, the shared person (mother, daughter, partner, professional caregiver)

- **Role:** Receives partial access to a primary user's profile via the shared panel (source § 7.5).
- **Goal:** Support/care without invading privacy.
- **JTBD:** *"Stay aware of [daughter/partner/mother] within the limits she allows me."*
- **Importance:** Retention lever and word-of-mouth acquisition vector.

### 2.3 Internal personas

#### P5 — **Dr. Elena**, clinical professional (dashboard 8.2)

- **Role:** Health professional on Itabey's clinical team.
- **Access:** Validation of biomedical content, criteria definition, knowledge versioning.
- **Restrictions:** No access to individual personal data, no access to conversations, no business metrics.

#### P6 — **Carla**, product/ops admin (dashboard 8.1)

- **Role:** Product administration, business metrics, content and moderation management.
- **Access:** Global system view, except individual conversations.

> **Cross-cutting note — Neurodivergent mode:** Not a persona, a **cross-cutting usage mode** that any persona (P1–P4) can activate (source § 14.2). Treated as a non-optional UX requirement for MVP (NFR-A).

> **Architectural note — P7, professional patient-management profile (Phase 3):** Distinct from **P5 — Dr. Elena** (who validates clinical knowledge for the entire system), a future persona **P7** represents professionals (clinicians, social workers, health *coaches*) who would access the system to manage several patients/users who have given them explicit consent. This persona **is not part of the MVP or Phase 2**, but the role and permission system (FR-1305, NFR-S04) and the granular consent model (FR-904) must architecturally enable it from the start.

---

## 3. Functional requirements

> **ID convention:** Groups are numbered by hundreds (FR-1xx, FR-2xx, …) by functional area. Each FR has a **Must / Should / Could** priority aligned with source § 26 (Critical / High / Future). Acceptance criteria are written as *observable, testable conditions*.

### 3.1 Data capture (FR-1xx)

#### FR-101 — Manual user data entry
- **Priority:** Must
- **Description:** The user can manually enter data on cycle, symptoms, emotions, habits, sleep, and events.
- **Trigger:** Explicit user action from main panel or calendar.
- **Expected outcome:** Data persisted, reflected in panel and calendar in < 2 seconds.
- **Acceptance criteria:**
  - Any entry persists offline and syncs upon connectivity recovery (offline-first, source § 4.1).
  - Data is editable and deletable by the user without restrictions.
  - Each data category has a structured schema (no opaque free text).

#### FR-102 — Structured voice-based entry
- **Priority:** Must
- **Description:** The user can update structured data through natural language by voice.
- **Trigger:** Wake-word activation or button.
- **Examples** (source § 6.2): *"Got my period today"*, *"My lower back hurts"*, *"I slept poorly"*, *"I'm very irritable"*.
- **Expected outcome:** The system interprets the phrase, extracts intent and entity, updates the corresponding structured data, and shows visual confirmation.
- **Acceptance criteria:**
  - Correct interpretation rate ≥ 90% on a Spanish and English test corpus.
  - Every interpretation is confirmable/correctable by the user before persistence.
  - Voice entry covers at minimum: cycle, localised pain, mood, sleep, events.

#### FR-103 — Voice-only mode
- **Priority:** Should
- **Description:** The application is navigable and operable using voice only.
- **Acceptance criteria:**
  - Core functionality (entry, Asha consultation, basic report generation) is accessible without touching the screen.
  - Compatibility with native screen readers (VoiceOver, TalkBack).

#### FR-104 — Wearable import (MVP)
- **Priority:** Must (Apple Health, Google Health Connect) / Should (rest)
- **Description:** Import biometric data from supported wearables.
- **MVP:** Apple Health, Google Health Connect.
- **Post-MVP:** Apple Watch, Oura Ring, Whoop, Fitbit, and equivalents.
- **Supported variables:** sleep, activity, heart rate, temperature, HRV, recovery, fatigue, training.
- **Acceptance criteria:**
  - User-revocable connection at any time.
  - Imported data clearly separated from manual data (source traceability).
  - Clear reconciliation when manual and wearable data exist for the same event.

#### FR-105 — External calendar event import
- **Priority:** Should (MVP / Phase 1)
- **Description:** One-way import of relevant events from Google Calendar and Apple Calendar (medical appointments, life events, travel) into the internal calendar panel (FR-303).
- **Acceptance criteria:**
  - User-driven activation, granular control of which calendars are read.
  - Configurable obfuscation of sensitive titles/descriptions before import.
  - Immediate deactivation; imported events removed on request.

#### FR-106 — Bidirectional external calendar sync (Phase 2)
- **Priority:** Should (Phase 2)
- **Description:** Bidirectional sync with Google Calendar and Apple Calendar that **publishes the cycle phase and selected relevant events** from the internal calendar to the user's external calendar, to facilitate planning without opening the app.
- **Acceptance criteria:**
  - **Configurable visualisation** in the external calendar: the user chooses among full invisibility, small discreet daily icon, colour code, text label, or combinations.
  - Sync of cycle phases (menstruation, estimated ovulation, estimated fertility, lunar phase if active) and, optionally, selected soft reminders.
  - **Privacy by default:** no sync at start — explicit, reversible opt-in.
  - **No** sensitive data is exported (symptoms, mood, Asha conversations) under any circumstances.
  - Immediate deactivation removes all exported events without retention.
  - Compatibility with shared calendars: the user controls whether exported events are visible to third parties sharing her calendar.

### 3.2 Asha conversational engine (FR-2xx)

#### FR-201 — Text conversation
- **Priority:** Must
- **Description:** Asha responds to natural-language text queries.
- **Acceptance criteria:**
  - Response in < 5 s (P95) for standard queries; < 10 s with deep RAG.
  - Each response complies with the structure in FR-205.

#### FR-202 — Voice conversation
- **Priority:** Must
- **Description:** Asha responds in voice with configurable voice, accent, speed, and tone.
- **Acceptance criteria:**
  - Voice-to-voice latency < 3 s (P95) for short responses.
  - Voice selectable by the user from a configurable catalogue.

#### FR-203 — RAG architecture
- **Priority:** 🛡️ **NON-NEGOTIABLE — Must**
- **Description:** Every Asha response relies on a controlled, validated, versioned knowledge base.
- **Acceptance criteria:**
  - 100% of biomedical-content responses internally cite the RAG source used (traceability).
  - Corpus version changes are auditable and reversible.
  - Hallucination control: if retrieval confidence is low, Asha downgrades the response to "I have no validated information on this" rather than generating freely.

#### FR-204 — Differentiated memory (short / long term)
- **Priority:** Must
- **Description:** Asha maintains short-term memory (current conversation) and long-term memory (patterns, preferences, useful conclusions).
- **Acceptance criteria:**
  - Full conversations are **not** stored as permanent memory by default.
  - Long-term memory is **selective** (patterns, relevant data, conclusions).
  - The user can inspect, edit, and delete long-term memory.

#### FR-205 — Asha response structure
- **Priority:** Must
- **Description:** Responses may include the following blocks:
  - Main answer
  - Contextual explanation
  - Practical suggestion
  - Optional educational capsule
  - Optional fact/curiosity
  - Content recommendation
  - Feedback button (FR-206)
  - Visible warning (FR-207)
- **Acceptance criteria:**
  - The "visible warning" block is **mandatory** in responses with health content.

#### FR-206 — User feedback per response
- **Priority:** Must
- **Description:** Each Asha response allows quick feedback: like / dislike / it helped / it didn't help / report / ask for simpler explanation / ask for more depth.
- **Acceptance criteria:**
  - Feedback feeds internal quality metrics **without exposing individual conversations**.
  - Feedback is reviewable by internal admin (Carla) in aggregate.

#### FR-207 — Visible, persistent disclaimers
- **Priority:** 🛡️ **NON-NEGOTIABLE — Must**
- **Description:** The interface visibly and persistently shows:
  - "Asha does not provide diagnoses."
  - "Asha does not replace a healthcare professional."
  - "Asha may make mistakes."
  - "For severe symptoms or medical doubts, consult a professional."
- **Acceptance criteria:**
  - Disclaimers present at: first response of each session, sensitive conversations, generated reports, health-related recommendations.

#### FR-208 — Hard-stop protocol
- **Priority:** 🛡️ **NON-NEGOTIABLE — Must**
- **Description:** Faced with severe risk signals (self-harm, intense emotional crisis, possible medical emergency), Asha **suspends generative response** and activates a predefined response oriented toward professional referral or emergency services.
- **Acceptance criteria:**
  - 100% of detected cases activate the predefined response (no free generation).
  - Each activation is logged for clinical audit with metadata: timestamp, signal type, resource offered.
  - The catalogue of signals and predefined responses is validated and versioned by the clinical team (FR-1002).

#### FR-209 — Generation of non-diagnostic hypotheses
- **Priority:** Must
- **Description:** Asha may generate non-clinical hypotheses, detect patterns, suggest observations, recommend professional consultation.
- **Restriction:** **Never** issues a diagnosis, **never** indicates personalised medical treatment.

#### FR-210 — Public Asha API (preparation)
- **Priority:** Should
- **Description:** Asha exposes a stable internal API that will, in the future, be exposed publicly for licensing.
- **Acceptance criteria:**
  - Asha is callable from outside the Itabey frontend via a documented API.
  - Semantic API versioning.
  - Coupling between Asha and Itabey occurs exclusively via this API (no shortcuts).

### 3.3 User panels (FR-3xx)

#### FR-301 — Main panel
- **Priority:** Must
- **Content:** Current state, contextual summary, quick access, Asha suggestions, upcoming relevant events, cycle phase, soft reminders, quick voice/text entry.

#### FR-302 — Self-knowledge panel
- **Priority:** Should (MVP) / Must (post-MVP)
- **Content:** Detected patterns, longitudinal evolution, comparisons across cycles and periods, improvement/worsening metrics, time-series charts, recommendation history, personal and dynamically suggested goals, completion tracking, Asha-generated insights.

#### FR-303 — Internal calendar panel
- **Priority:** Must
- **Description:** Itabey's own calendar. The **canonical view** of the user's cyclical information inside the app — all longitudinal cycle data lives here.
- **Content:** Hormonal cycle, menstruation, estimated ovulation, estimated fertility, energy states, lunar phase, manual events, relevant symptoms, soft predictions, configuration of visible elements.
- **Explicit distinction:** Sync with external calendars (Google/Apple) is not part of this FR. It is specified separately in FR-105 (event import, MVP) and FR-106 (bidirectional sync with cycle phase visualisation in the external calendar, Phase 2).

#### FR-304 — Body panel
- **Priority:** Should
- **Content:** Interactive body map (3D or pseudo-3D), zone selection, pain/symptom logging by zone, temporal evolution, educational explanation, association with cycle/habits/sleep/stress.

#### FR-305 — Shared panel
- **Priority:** Should
- **Description:** The user can share information granularly and temporarily with: partner, mother/daughter, healthcare professional, authorised carer.
- **Acceptance criteria:**
  - The user controls **what** she shares, **for how long**, and **with whom**.
  - Immediate revocation without consequences for the data.

### 3.4 Reports and export (FR-4xx)

#### FR-401 — Reports for the user
- **Priority:** Must
- **Content:** Longitudinal evolution, symptoms, cycle, emotional state, patterns, goals, recommendations, comparatives, charts.
- **Formats:** PDF minimum in MVP.

#### FR-402 — Reports for professionals
- **Priority:** Should
- **Content:** Structured clinical summary, symptoms by period, observed correlations, cycle evolution, relevant entries, history, life events, preparation for medical consultation.
- **Acceptance criteria:**
  - Format intended for printing and delivery in consultation (no professional login required).
  - Clear identification that the document is generated by Itabey and does not constitute a diagnosis.

#### FR-403 — Reports from Asha conversation
- **Priority:** Should
- **Description:** The user may request:
  - *"Give me a summary of this conversation."*
  - *"Prepare this for my doctor."*
  - *"Convert this into a report."*
  - *"Save this conclusion."*
- **Acceptance criteria:**
  - Downloadable PDF (minimum) with timestamp and disclaimer.
  - User reviews and approves before download.

### 3.5 Community and educational content (FR-5xx)

#### FR-501 — Moderated community
- **Priority:** Should (near post-MVP)
- **Functionality:** Posts, comments, optional anonymity, categories, reports, manual + AI-assisted moderation, sensitive-content filtering, user blocking, moderation history, aggregated recommendations.
- **Restrictions:**
  - Asha **does not** expose individual data when recommending community content.
  - Proactive detection and blocking of spam, misinformation, and conflict.

#### FR-502 — Educational content capsules
- **Priority:** Must (MVP with limited initial catalogue)
- **Description:** Information capsules by symptom, cycle phase, emotional state, need.
- **Acceptance criteria:**
  - All biomedical content is validated and versioned by the clinical team before publication.
  - Capsules feed Asha's RAG base.

#### FR-503 — Podcast recommendations (preparation)
- **Priority:** Could (depends on prior podcast existence — open question to CEO)
- **Description:** Episode and fragment recommendations; automatic transcription; indexing.

### 3.6 Personalisation (FR-6xx)

#### FR-601 — Asha personalisation
- **Priority:** Must
- **Configurable:** Tone (direct, empathetic, technical, realistic, soft, structured), personality, depth level, style, voice, accent, speed, preferred focus.

#### FR-602 — Language levels
- **Priority:** Must
- **Levels:** Simple, technical, advanced.
- **Acceptance criteria:**
  - User changes level at any time, in any conversation.
  - Educational capsules exist at least in Simple and Technical levels.

#### FR-603 — Activatable focus modules
- **Priority:** Should
- **Focuses:** Scientific, integrative, emotional, wellbeing, spiritual, complementary.
- **Restriction:** Complementary focuses are presented as **optional layers of observation**, neither replacing medicine nor positioned at the same evidence level.

### 3.7 Onboarding (FR-7xx)

#### FR-701 — Progressive conversational onboarding
- **Priority:** Must
- **Steps:** Profile creation, initial configuration, focus selection, Asha tone selection, language level selection, privacy explanation, consent, introduction to functioning, progressive feature activation.
- **Acceptance criteria:**
  - No onboarding step overwhelms the user with > 3 simultaneous decisions.
  - Consent is granular (no global checkbox) and revocable.

#### FR-702 — In-product explanatory video
- **Priority:** Should (MVP)
- **Description:** Short video (< 3 min) explaining how the app works, accessible from the onboarding flow (skippable) and from a permanent help menu (re-watchable on demand).
- **Acceptance criteria:**
  - Available at least in Spanish and English (NFR-I01).
  - Closed captions (CC) toggleable by default (NFR-A03).
  - Skippable at any time during onboarding without flow penalty.
  - Re-watchable from help menu → "How does Itabey work?".
  - Plays offline if cached.
- **Scope note:** This FR covers the player, in-product integration, and accessibility. **Production of video content** (script, voiceover, animation) is the responsibility of the development vendor or a contracted content vendor — to be made explicit in budget (E13) if delegated.

### 3.8 Notifications (FR-8xx)

#### FR-801 — Soft notifications system
- **Priority:** Should
- **Types:** Reminders, contextual alerts, suggestions, anticipatory preparation, goal tracking, cycle alerts, content recommendations, incomplete-record alerts.
- **Acceptance criteria:**
  - User adjusts frequency, type, and intervention level.
  - Non-invasive notifications by default (opt-in for specific types).

### 3.9 Privacy and data control (FR-9xx)

#### FR-901 — Visibility of stored data
- **Priority:** 🛡️ **NON-NEGOTIABLE — Must**
- The user can see at any time which data is stored about her.

#### FR-902 — Data export
- **Priority:** 🛡️ **NON-NEGOTIABLE — Must**
- Full export in structured format (JSON + summary PDF).

#### FR-903 — Data deletion / right to be forgotten
- **Priority:** 🛡️ **NON-NEGOTIABLE — Must**
- Total deletion with explicit confirmation; technical traceability of deletion for audit without retaining content.

#### FR-904 — Granular consent control
- **Priority:** 🛡️ **NON-NEGOTIABLE — Must**
- Independent activation/deactivation for: Asha memory, aggregate use for research, integrations, sharing (shared panel), specific notifications.

#### FR-905 — Pause tracking
- **Priority:** Must
- The user can pause tracking (without deletion) and resume later.

### 3.10 Internal dashboards (FR-10xx)

#### FR-1001 — Administration dashboard
- **Priority:** Must (MVP minimal view) / Should (full view)
- **Content (full view):** Total users, DAU/WAU/MAU, signups, churn, retention, geographical distribution, feature usage, most-used modules, frequent Asha questions, consulted topics, educational content metrics, aggregate community metrics, incidents, alerts, content control, capsule management, notification activation, feature control, knowledge versioning, change history, approval traceability, internal audit.
- **MVP minimal view:** Total users, MAU, aggregate retention, critical incidents.

#### FR-1002 — Clinical dashboard
- **Priority:** Must (partial MVP) / Should (full)
- **Access:** Restricted to healthcare professionals.
- **Allows:** Entering structured clinical knowledge, validating biomedical content, approving educational capsules, defining general criteria, validating correlations, proposing clinical variables, defining referral criteria, reviewing protocols, versioning knowledge.
- **Restrictions:**
  - **No** access to individual personal data.
  - **No** access to individual conversations.
  - **No** access to business metrics.
  - **No** operational control of the system.
  - **No** ability to modify product or global configuration.

#### FR-1003 — Analytics dashboard
- **Priority:** Should
- **Content:** Usage behaviour, cohorts, retention, population patterns, longitudinal trends, data quality, Asha performance, educational content impact, hypothesis validation, anonymised dataset export with prior consent.

#### FR-1004 — Community moderation dashboard
- **Priority:** Should (coupled with FR-501)
- **Content:** Post and comment management, reported content, manual + AI-assisted moderation, sensitive-content detection, temporary user blocks, anti-spam tools, history, metrics, conflict alerts.

#### FR-1005 — Technical supervision panel
- **Priority:** Should
- **Access:** Read-only for senior technical supervision.
- **Content:** Overall system status, availability, performance, critical incidents, integration status, aggregate technical metrics, general Asha usage, relevant alerts.
- **Restrictions:** No code edits, no structural changes, no operational control, no access to individual personal data, no access to conversations.

### 3.11 External integrations (FR-11xx)

#### FR-1101 — Integration with health platforms (MVP)
- **Priority:** Must
- **MVP integrations:** Apple Health, Google Health Connect.
- **Variables:** sleep, activity, heart rate, temperature, HRV.

#### FR-1102 — Integration with external calendars (umbrella)
- **Priority:** Should (MVP covers only import — FR-105) / Should (Phase 2 completes — FR-106)
- **Integrations:** Google Calendar, Apple Calendar (via official APIs and, where applicable, CalDAV).
- **Operationalises:** FR-105 (import) and FR-106 (bidirectional sync with cycle phase visualisation).
- **Cross-cutting criteria:** User-driven activation, granular configuration, immediate deactivation, privacy by default.

#### FR-1103 — Open architecture for future integrations
- **Priority:** Must (architectural preparation)
- **Description:** The architecture allows incorporation of Apple Watch, Oura, Whoop, Fitbit, and cycle/habit/health apps without structural redesign.
- **Standards mapping:** HL7/FHIR not required in MVP, but the internal structure must allow mapping to these standards in later phases.

### 3.12 Risk detection and referral (FR-12xx)

#### FR-1201 — Detection and referral protocols
- **Priority:** 🛡️ **NON-NEGOTIABLE — Must**
- **Detected signals:** Severe emotional risk, concerning medical symptoms, crisis signals, self-harm, marked deterioration, high-vulnerability patterns.
- **Expected behaviour:** Automatic activation of hard-stop (FR-208) with predefined responses, professional referral, emergency resources.
- **Acceptance criteria:**
  - Signal catalogue clinically validated before deployment.
  - 0 critical false negatives in controlled testing (severe signals not detected).
  - < 5% false positives (tolerable: better to err cautious).

### 3.13 Account management, access modes, and tiers (FR-13xx)

> Cross-cutting functionality and architectural commitment. Operationalises § 1.5: the user account is a single persistent object; commercial access mode and functional depth are **two orthogonal axes** (access mode × depth tier), both modulable without data loss.

#### FR-1301 — Single persistent user account
- **Priority:** Must (MVP)
- **Description:** Each user owns a **single** account linked to her identity and longitudinal data. The account survives any change of access mode (free → individual, individual → B2B, B2B → individual at end of organisational contract) and any tier change.
- **Acceptance criteria:**
  - No account duplication on mode or tier change.
  - 100% of longitudinal data preserved on mode or tier change.
  - The user is **always the data owner**. The paying organisation is not the owner and cannot inherit the account.

#### FR-1302 — Commercial access modes
- **Priority:** Must (free + individual MVP) / Should (B2B in Phase 2)
- **Modes:**
  - **Free** — limited functionality (source § 2).
  - **Paid individual** — paid directly by the user.
  - **Organisation-sponsored (B2B)** — paid by a company, insurer, mutual, healthcare system, or other entity. Linkage via code, invitation, or enterprise SSO.
- **Acceptance criteria:**
  - The active mode is visible to the user at any time.
  - Mode change does not require re-onboarding or new consent for existing data.

#### FR-1303 — Mode migration without data loss
- **Priority:** Must (free ↔ individual in MVP) / Should (including B2B in Phase 2)
- **Cases covered:**
  - **Free → Individual:** feature unlocking; previous data immediately accessible.
  - **Individual → B2B:** the organisation assumes the cost; the user keeps account, data, and configuration.
  - **B2B → Individual:** at end of organisational contract, the user receives advance notice and chooses to continue as paid individual or downgrade to free with data preserved.
  - **Any mode → Free:** data is not deleted unless explicitly requested; some features become inaccessible but data remains exportable.
- **Acceptance criteria:**
  - Migration completed in < 5 minutes without technical intervention.
  - 100% of data preserved (entries, Asha memory, configurations, integrations).
  - Migration traceability in audit logs.

#### FR-1304 — B2B mode privacy
- **Priority:** 🛡️ **NON-NEGOTIABLE — Must (when B2B is delivered)**
- **Description:** When an organisation sponsors a user's access, the organisation **never accesses** that user's personal data or individual conversations.
- **Acceptance criteria:**
  - The organisation only accesses aggregated, anonymous metrics (overall usage, aggregate satisfaction, cohort trends). Never individual.
  - Any additional sharing (e.g. sending a report) requires explicit, revocable user action.
  - Technically auditable: a malicious organisation can never correlate usage with individual identity.
  - Minimum cohort size for aggregate reports (≥ 10 active users, proposal) to prevent re-identification by inference.

#### FR-1305 — Professional patient-management profile (Phase 3 — architectural preparation)
- **Priority:** Could (not built in MVP or Phase 2)
- **Description:** Reserve the possibility of a professional profile (clinician, social worker, health *coach*) able to manage several users/patients who have given explicit consent.
- **Architectural acceptance criteria (required of MVP vendor):**
  - The role and permission system (source § 20, NFR-S04) allows incorporating this role without structural redesign.
  - The consent model (FR-904) lets the user authorise a specific professional's access to a granular subset of her data for a configurable period.
  - The data model anticipates an N-to-M relation between professional managers and users.
- **Distinction from P5 (Dr. Elena):** P5 validates generic clinical knowledge for the entire system. P7 (this future profile) manages individual patients with explicit consent.

#### FR-1306 — Functional depth tiers (architectural capability)
- **Priority:** Must (MVP architectural capability) / Should (operational tiers Phase 2)
- **Description:** The system supports **distinct functional depth tiers** that can be activated or deactivated by user, cohort, or contract without code changes. The PRD **does not prescribe** which features belong to which tier — that decision is deferred to product based on real usage signal. What is required is the **architectural capability** from day 1.
- **Per-tier parameterisable axes (non-exhaustive):**
  - Asha **long-term memory** depth (FR-204): time horizon, simultaneous patterns, pattern granularity.
  - **Insight frequency and depth** (FR-209): proactive vs on-demand only.
  - **Asha personalisation** (FR-601): number of available tones, language levels, focus modules (FR-603).
  - **Access to advanced panels** (FR-302 self-knowledge, FR-304 body): visibility and depth.
  - **Available integrations** (FR-104, FR-1101–1103): which wearables and calendars connect.
  - **Report volume** (FR-401–403): number, frequency, format.
  - **Resource consumption quotas**: LLM calls, vector storage, tokens, voice processing.
- **Acceptance criteria:**
  - Any § 3 feature can be enabled/disabled per tier via configuration (not by code deployment).
  - Every tier has **defined and observable resource quotas**; no tier is "unlimited" without a cap.
  - Tier change is transparent to the user (data intact, configurations preserved) and reversible.
  - At least **3 parameterisable tiers** supported from the MVP (concrete names and contents to be defined later by product/commercial).

#### FR-1307 — Dynamic feature activation (feature flags as a capability)
- **Priority:** Must (MVP)
- **Description:** The system has a **first-class feature flag manager** that allows:
  - Activating/deactivating features by user, cohort, tier (FR-1306), access mode (FR-1302), or rollout percentage.
  - Testing features in production with a subset of users before global enablement (canary release, A/B testing).
  - Fast rollback without redeploy if a feature causes incidents.
- **Acceptance criteria:**
  - A flag change propagates to the client in < 60 seconds without app restart.
  - There is an **admin panel** (linked to FR-1001) for flag management with full change audit.
  - Flags **are not** used to bypass disclaimers, hard-stop, or non-negotiable privacy/security requirements.
  - The system functions correctly with any coherent combination of active/inactive flags.

---

## 4. Non-functional requirements

### 4.1 Performance (NFR-P)

| ID | Requirement | Target |
|----|-------------|--------|
| NFR-P01 | Asha text response (P95) | < 5 s standard query; < 10 s deep RAG query |
| NFR-P02 | Asha voice response (P95) | < 3 s for short responses |
| NFR-P03 | Initial app load (P95) | < 3 s on 4G network |
| NFR-P04 | Manual entry persistence | < 2 s visual confirmation |
| NFR-P05 | PDF report generation | < 30 s for 90 days of data |

### 4.2 Reliability (NFR-R)

| ID | Requirement | Target |
|----|-------------|--------|
| NFR-R01 | Monthly availability | ≥ 99.5% (post-launch) |
| NFR-R02 | Offline-first operation of entry | 100% of core entry functionality offline |
| NFR-R03 | Fallback for Asha or external integration failure | Application stays operational with clear message and local entries preserved |
| NFR-R04 | Disaster recovery | RTO < 4 h, RPO < 1 h (post-launch) |
| NFR-R05 | Backups | Encrypted daily backup in separate European repository |

### 4.3 Security (NFR-S)

| ID | Requirement |
|----|-------------|
| NFR-S01 | TLS 1.3 minimum for data in transit |
| NFR-S02 | AES-256 (or equivalent) for data at rest |
| NFR-S03 | Strong authentication (minimum email + password with modern policies; MFA optional MVP, mandatory for internal roles) |
| NFR-S04 | RBAC role-based access control (source § 20) |
| NFR-S05 | Activity logs and internal access audit |
| NFR-S06 | Full traceability of critical changes (knowledge versioning, consent changes, access by clinical role) |
| NFR-S07 | Module isolation (Itabey ↔ Asha via API) |
| NFR-S08 | Protection against unauthorised access (rate-limiting, anomaly detection) |
| NFR-S09 | Proactive incident monitoring |
| NFR-S10 | Design ready for external security audits |
| NFR-S11 | Secure secrets management (no hardcoding, managed vault) |
| NFR-S12 | Regular security testing (DAST/SAST, pen-test before each major release) |

### 4.4 Privacy (NFR-PR)

| ID | Requirement |
|----|-------------|
| NFR-PR01 | 🛡️ GDPR compliance with Art. 9 treatment of health data |
| NFR-PR02 | 🛡️ Explicit, granular, revocable consent |
| NFR-PR03 | 🛡️ Data minimisation: only what is needed for the active feature |
| NFR-PR04 | 🛡️ Anonymisation or pseudonymisation for aggregate use |
| NFR-PR05 | 🛡️ Architectural separation between individual and aggregate data |
| NFR-PR06 | 🛡️ Right to be forgotten implemented at pipeline level (not soft-delete only) |
| NFR-PR07 | 🛡️ No sale of personal data under any circumstances |
| NFR-PR08 | DPIA conducted before launch |

### 4.5 Compatibility (NFR-C)

| ID | Requirement |
|----|-------------|
| NFR-C01 | iOS 16+ and Android 12+ in MVP |
| NFR-C02 | Responsive web (Chrome, Safari, Firefox, Edge versions N and N-1) |
| NFR-C03 | Screen-reader compatibility (VoiceOver, TalkBack, NVDA) |
| NFR-C04 | Apple Health (iOS) and Google Health Connect (Android) compatibility |

### 4.6 Scalability (NFR-SC)

| ID | Requirement | Target |
|----|-------------|--------|
| NFR-SC01 | Year 1 registered users | 10,000–30,000 (source § 21) |
| NFR-SC02 | Year 1 monthly active users | 3,000–10,000 |
| NFR-SC03 | Growth capacity without structural redesign | Up to 50,000 users |
| NFR-SC04 | Modular architecture with feature flags |
| NFR-SC05 | Progressive rollout and functional rollback |
| NFR-SC06 | **Functional modularity as a first-class architectural capability** — every § 3 feature activatable/deactivatable via configuration (FR-1306, FR-1307). No rigid dependencies that would prevent tiering. |
| NFR-SC07 | **Per-tier resource quotas** (LLM, vector storage, tokens, voice) configurable and observable without code changes |

### 4.7 Accessibility (NFR-A)

| ID | Requirement |
|----|-------------|
| NFR-A01 | WCAG 2.1 AA minimum |
| NFR-A02 | Voice-only mode (FR-103) |
| NFR-A03 | Compatibility with non-sighted users |
| NFR-A04 | Activatable neurodivergent mode: stimulus reduction, simplified navigation, clear hierarchy, no intense animations, contrast control, legible typography, guided flows, low cognitive load |
| NFR-A05 | Usage modes: crisis, real life, light support |
| NFR-A06 | Dark mode as full visual adaptation (not simplification) |

### 4.8 Internationalisation (NFR-I)

| ID | Requirement |
|----|-------------|
| NFR-I01 | MVP supports Spanish and English |
| NFR-I02 | Architecture ready to add languages without redesign |
| NFR-I03 | Educational content, interface, and conversational engine independently translatable |

### 4.9 Deployment and data sovereignty

| ID | Requirement |
|----|-------------|
| NFR-D01 | 🛡️ Deployment in European cloud (specific provider proposed by vendor) |
| NFR-D02 | Personal data processing within the EU |
| NFR-D03 | Subprocessor documentation with international transfer justification if any |

### 4.10 Support, maintenance, and post-launch operations

| ID | Requirement |
|----|-------------|
| NFR-M01 | Evolutionary and corrective maintenance plan documented by vendor (see E9) |
| NFR-M02 | Incident response times defined by severity (vendor-proposed; minimum target: critical < 4 h, high < 24 h, medium < 5 working days) |
| NFR-M03 | Technical support available at least during European business hours |
| NFR-M04 | Recurring monthly cost broken down: infrastructure, LLM models, voice, vector storage, human support (E14) |
| NFR-M05 | Cost estimation by scenario per 1,000 active users (low, medium, high) — preserves source § 18.5 requirement |
| NFR-M06 | Documented exit plan **anti vendor lock-in** (E16): how Itabey would continue without the vendor in fewer than N weeks |
| NFR-M07 | Operational runbooks for frequent incidents delivered at project closure |
| NFR-M08 | Critical security updates with specific SLA (target: < 72 h post-detection) |
| NFR-M09 | **Documented HL7/FHIR readiness** (E15): data model mapping to these standards and evolution plan without structural redesign — required in initial proposal even though implementation is Phase 3 |
| NFR-M10 | Commitment to update tiers (FR-1306) and feature flags (FR-1307) runbook every time the feature matrix changes |

---

## 5. User flows (primary flows)

### 5.1 F1 — Day 1 onboarding

**Personas:** P1, P2, P3.

1. User downloads the app and logs in / signs up.
2. Privacy screen: clear explanation of data treatment (GDPR Art. 9); granular consents (Asha memory, integrations, aggregate use, shared panel).
3. **Focus** selection (scientific, integrative, emotional, wellbeing, spiritual, complementary — multi-select allowed).
4. Asha **tone** and **language level** selection.
5. Conversational mini-tutorial: Asha introduces herself, explains limits (FR-207), invites first entry.
6. Assisted first entry (manual or voice).
7. First contextual Asha response + mandatory disclaimer.
8. Suggestion to set up wearable and calendar integration (skippable).

**Success criterion:** ≥ 70% of users complete onboarding in one session.

### 5.2 F2 — Daily entry (golden path)

**Personas:** P1, P2, P3.

1. Soft notification (configurable) or spontaneous user entry.
2. Voice (preferred) or text input: *"Got my period today."*
3. Asha extracts intent + entity, shows structured visual confirmation.
4. User confirms or corrects.
5. Data persisted (offline if no network), reflected in main panel and calendar.
6. (Optional) Asha suggests consultation or contextual capsule.

**Success criterion:** Full entry in < 30 s (P95).

### 5.3 F3 — Longitudinal pattern consultation

**Personas:** P1, P2, P3.

1. User opens self-knowledge panel.
2. Detected pattern: "Your energy drops recurrently 2 days before your cycle."
3. User taps the pattern → Asha contextualises with validated RAG.
4. Asha recommends educational capsule or logs an observation.
5. User optionally adds personal goal or shares the pattern.

**Success criterion:** ≥ 50% of monthly active users open the self-knowledge panel at least once a month.

### 5.4 F4 — Generating a report for a healthcare professional

**Personas:** P2 (critical), P1, P3.

1. User asks Asha (voice or text): *"Prepare a report for my doctor."*
2. Asha requests time range and focus (symptoms, cycle, mood, all).
3. Asha generates structured clinical summary: symptoms by period, correlations, evolution, relevant entries.
4. User reviews, edits optional fields, confirms.
5. System generates signed/timestamped PDF with mandatory disclaimer.
6. Direct download or secure send.

**Success criterion:** ≥ 30% of P2 users generate at least one report in 90 days.

### 5.5 F5 — Hard-stop / crisis (cross-cutting non-negotiable)

**Personas:** Anyone.

1. User expresses a severe signal (self-harm, crisis, medical emergency) by text or voice.
2. **System detects signal and immediately suspends Asha's generative response.**
3. Asha responds with a clinically validated predefined message.
4. System shows localised emergency resources (European 112, country-specific crisis lines).
5. Asha offers (with consent) to contact a preconfigured trusted person or healthcare professional.
6. System logs the event for clinical audit with metadata (no conversational content).

**Success criterion:** 100% of severe signals activate hard-stop. 0 incidents of free generative response to a severe signal.

---

## 6. Constraints, assumptions, and dependencies

### 6.1 Technical constraints

| ID | Constraint |
|----|------------|
| TC1 | 🛡️ European cloud deployment |
| TC2 | 🛡️ Standard, maintainable tech stack — vendor proposes, justifies, avoids proprietary lock-in |
| TC3 | 🛡️ Asha decoupled from Itabey (API access) from day 1 |
| TC4 | Offline-first for data entry |
| TC5 | Multilingual Spanish + English from MVP |

### 6.2 Business constraints

| ID | Constraint |
|----|------------|
| BC1 | Freemium model: limited free version + paid version with advanced features |
| BC2 | No personal data sale |
| BC3 | Full intellectual property to Itabey (source § 24): code, architecture, prompts, embeddings, derived weights, RAG configurations, etc. |
| BC4 | Mandatory NDA and confidentiality with development vendor |
| BC5 | Multidisciplinary clinical team validates all biomedical content |

### 6.3 Regulatory constraints

| ID | Constraint |
|----|------------|
| RC1 | 🛡️ Full GDPR compliance, including Art. 9 (health data) |
| RC2 | 🛡️ Asha is **not** a medical device. No diagnosis, no prescription, no professional substitution |
| RC3 | DPIA before launch |
| RC4 | Subprocessor and international transfer documentation if any |

### 6.4 Assumptions

| ID | Assumption | Risk if false |
|----|------------|---------------|
| A1 | Clinical team will be available before MVP to validate the initial knowledge base | Without validated content, the RAG engine cannot respond safely |
| A2 | GDPR compliance allows European cloud processing without additional transfers | Any non-EU service dependency complicates compliance |
| A3 | Seed traction hypothesis assumes organic growth + modest paid acquisition | Metrics may need revision if acquisition strategy changes |
| A4 | Initial capsule catalogue (≥ 30) available or developed in parallel with the product | Without content, educational panel and RAG base are empty |
| A5 | Primary market is Spain + EU (NFR-I01 OK) | If LATAM is a Year 1 target, legal and deployment implications apply |

### 6.5 External dependencies

- Apple Health Kit, Google Health Connect (current SDK and terms).
- Google Calendar API, Apple Calendar API.
- European cloud provider (to propose).
- LLM and embeddings vendor (to propose; with no-training commitments on data).
- Voice vendor (TTS/STT) (to propose).
- Multidisciplinary clinical team contracted/identified by Itabey.

---

## 7. Success metrics

> 🏷️ **PROPOSAL — all target values require CEO validation.** Ranges are aligned with public benchmarks for longitudinal B2C healthtech and cycle apps (Flo, Clue, Natural Cycles) adjusted to Itabey's expected usage profile.

### 7.1 Activation

| Metric | Target | Measurement |
|--------|--------|-------------|
| % users completing onboarding | ≥ 70% | Funnel analytics events |
| % users with ≥ 7 days of entry in week 1 | ≥ 40% | Per-user entry events |
| Time to first useful Asha "insight" (self-reported or positive feedback) | < 72 h | First positive feedback timestamp |

### 7.2 Retention

| Metric | Target |
|--------|--------|
| D7 retention | 45% |
| D30 retention | 25% |
| D90 retention | 15% |
| Days with entry / month (active users) | ≥ 12 |

### 7.3 Asha quality

| Metric | Target |
|--------|--------|
| % responses with positive feedback | ≥ 65% |
| % responses reported as problematic | < 2% |
| Rate of "I don't know" (low-confidence RAG) over total | Monitored, no fixed target |

### 7.4 Clinical safety (critical — non-negotiable)

| Metric | Target |
|--------|--------|
| 🛡️ Unauthorised diagnostic response incidents | **0** |
| 🛡️ Correct hard-stop activation on severe signals | **100%** |
| Mean time for clinical capsule validation | < 14 days |
| Critical false negatives in risk detection (testing) | **0** |

### 7.5 Business

| Metric | Target |
|--------|--------|
| Free → paid conversion | 5–8% |
| Monthly paid churn | < 5% |
| LTV / CAC | ≥ 3 (post-launch at 6 months) |

### 7.6 Scale (source § 21 — CEO figures)

| Metric | Target |
|--------|--------|
| Year 1 registered users | 10,000–30,000 |
| Year 1 MAU | 3,000–10,000 |
| No-redesign capacity | 50,000 |

### 7.7 Community and content (near post-MVP)

| Metric | Target |
|--------|--------|
| Forum DAU/MAU | ≥ 0.2 |
| Mean moderation time | < 24 h |
| Validated educational capsules / quarter | ≥ 15 |

---

## 8. Risks

| ID | Risk | Probability | Impact | Mitigation |
|----|------|-------------|--------|------------|
| R1 | Asha emits content interpretable as diagnosis (hallucination, *jailbreak*, edge case) | M | Critical (legal + reputational + clinical) | Strict RAG, hard-stop, visible disclaimers, clinical audit, red-teaming before launch |
| R2 | Sensitive data leak (GDPR Art. 9) | L | Critical (legal + reputational) | In-transit and at-rest encryption, layer segregation, pen-test, monitoring, least-privilege policy |
| R3 | Clinical team unavailable in time or insufficient | M | High (blocks base content) | Early hiring, clear load definition, schedule slack |
| R4 | LLM inference costs grow above expectations | M | Medium | Per-scenario estimation (source § 18.5), caching, layered models (large model only when RAG justifies), free-tier per-user caps |
| R5 | Excessive dependency on a single LLM vendor | M | Medium | Clear exit clauses, model abstraction layer, demonstrated portability in architecture |
| R6 | Community moderation crisis | M | Medium | Proactive manual + AI moderation, clear policy, fast-block capability |
| R7 | Hard-stop false positives frustrate users | H | Low | Clinically validated catalogue, empathetic message on false positive, "this wasn't a crisis" feedback mechanism |
| R8 | Vendor technical lock-in on switch | M | High | Full IP clauses, contractual documentation, deliverable source code and architecture |
| R9 | User base rejects paid model | M | Medium | A/B test tiers, generous freemium, willingness-to-pay study |
| R10 | Insufficient GDPR compliance detected in audit | L | Critical | Early DPIA, EU-healthtech specialist legal advice, external audit before launch |
| R11 | Vendor delivers monolithic architecture that hinders later tiering | M | High | Modularity and feature flags as evaluation criteria (FR-1306–1307, NFR-SC06–07, § 12.4); rejection of proposals lacking demonstration |
| R12 | B2B negotiates low volume prices while infrastructure/AI costs grow | M | High | Per-tier resource quotas from MVP (NFR-SC07), B2B pricing models based on consumption beyond per-seat, B2B tier with limited depth by default |
| R13 | B2C *power users* consume disproportionate resources in standard tier | M | Medium | Clear per-tier quotas (FR-1306), upgrade path to premium tier with cost aligned to delivered value |
| R14 | Tier strategy defined late, forcing product rebuild | L | High | Architectural capability from MVP (FR-1306–1307); commercial tier-content decision can be made at any time without redesign |

Probability: H/M/L. Impact: Critical/High/Medium/Low.

---

## 9. Verification strategy

> Mandatory PRD section: *"How will we know this is actually done — not just reported as done?"*

### 9.1 Functional verification

- **Automated tests** per FR — coverage ≥ 80% on critical flows (entry, hard-stop, report generation).
- **Manual exploratory testing** per release with a script based on flows F1–F5.
- **Automated regression testing** in CI/CD pipeline.

### 9.2 Security and privacy verification

- **DAST/SAST** in every release.
- **External pen-test** before general launch and annually.
- **Documented GDPR audit** before launch.
- **DPIA** with specialised legal review.

### 9.3 Clinical verification

- **Clinical team reviews** every educational capsule before publication (FR-1002).
- **Hard-stop catalogue** reviewed and signed off by clinical team.
- **Clinical red-teaming** before launch: simulation of edge cases (self-harm, critical symptoms, emotional pressure) on Asha in staging.
- **Risk-detection testing** (FR-1201) on validated test corpus: 0 critical false negatives.

### 9.4 Asha quality verification

- **Automated RAG eval suite**: retrieval precision, *answer faithfulness* (citation grounding), hallucination rate detected by judge.
- **Production feedback**: continuous FR-206 monitoring, alarm if % negative feedback exceeds threshold.
- **Weekly review** of anonymised samples of problematic responses.

### 9.5 UX and accessibility verification

- **WCAG 2.1 AA audit** before launch.
- **Real-user testing** representative of P1, P2, P3 (minimum 5 per persona).
- **Neurodivergent mode testing** with users in that profile.

### 9.6 Operational verification

- **Documented and rehearsed incident response plan**.
- **Runbooks** for Asha failures, integrations, hard-stop.
- **Observable metrics** (NFR-P, NFR-R) on 24/7 dashboards.

---

## 10. Glossary

| Term | Definition |
|------|------------|
| **Asha** | Itabey's conversational engine. Interpretive intelligence based on RAG over validated clinical knowledge. Does not diagnose. |
| **Educational capsule** | Short, clinically validated, versioned piece of educational content that feeds both the interface and the RAG base. |
| **Hard-stop** | Generative-response suspension protocol on severe signals. Activates predefined, clinically validated messages. |
| **Non-diagnostic hypothesis** | Observation or pattern Asha can communicate without asserting a clinical cause or recommending specific treatment. |
| **Crisis mode** | Simplified usage mode for emotionally or symptomatically heavy days. |
| **Neurodivergent mode** | Cross-cutting UX mode with stimulus reduction, simplified navigation, low cognitive load. |
| **Selective memory** | Asha storage policy: keeps useful patterns and conclusions, **not** full conversations. |
| **Shared panel** | Functionality that lets the user share information granularly and temporarily with authorised third parties. |
| **RAG (Retrieval-Augmented Generation)** | Architecture where generative responses rely on a controlled, versioned external knowledge base. |
| **Pseudonymisation** | Data protection technique replacing direct identifiers with pseudonyms. Under GDPR, still personal data. |
| **Anonymisation** | Technique that prevents identification, irreversibly. Under GDPR, anonymised data is no longer personal. |
| **Privacy by design** | Principle that privacy is embedded from design and by default, not added at the end. |
| **Security by design** | Analogue: security is integrated from the architecture, not patched. |

---

## 11. Open questions for the CEO

> **Important:** These questions need a CEO answer before development tickets are generated. Some affect technical architecture and metrics. Recommendation: group them in a single conversation to avoid fragmentation.

| ID | Question | Why it matters |
|----|----------|----------------|
| Q1 | What traction hypothesis was presented to investors at seed (€1.5M)? | Without it, § 7 KPIs are generic benchmarks, not validated commitments |
| Q2 | Is the primary market Spain, full EU, or is LATAM contemplated for Year 1? | Changes mandatory languages, additional regulation, cloud deployment |
| Q3 | Is the multidisciplinary clinical team already identified/contracted, or is helping to recruit it part of the vendor's scope? | Substantially changes budget and schedule |
| Q4 | Does the podcast (source § 10) exist with produced content, or is it created alongside the product? | If absent, FR-503 leaves the MVP |
| Q5 | Sports vertical (source § 23): 18-month or 36+-month horizon? | Determines architectural surface to reserve |
| Q6 | The 2026-05-08 CEO feedback signals: the defensible asset is the **combination of common core (UX + knowledge base + RAG engine) and the modular tiering capability** that differentiates depth per user. Confirm this reading? | The answer validates the architectural emphasis of § 1.5, NFR-SC06–07, and the evaluation criteria § 12.4 |
| Q7 | Is there a cost ceiling for the MVP, or is the proposal open to vendor? | Defines a realistic MVP scope |
| Q8 | LLM model policy: private, open-source self-hosted, mixed? | Critical implications on privacy and cost |
| Q9 | When will the **concrete tier contents** be defined (which features in core/standard/premium, which for B2B vs B2C)? Suggestion: after 3 months of real usage with a validation cohort. | Allows product/commercial to plan the decision without blocking development |
| Q10 | What minimum B2B cohort is acceptable to guarantee aggregate privacy (FR-1304)? MVP proposal: ≥ 10 active users for aggregate reports. | Below a certain size, re-identification by inference becomes feasible |

---

## 12. Vendor evaluation criteria

> This section operationalises source § 25 so that received proposals can be compared structurally.

### 12.1 Required demonstrable capabilities

- Development of scalable mobile + web applications (verifiable references).
- HealthTech or sensitive-data treatment (GDPR Art. 9).
- GDPR compliance, Privacy/Security by design.
- Conversational AI with RAG architecture in production.
- Integration with external APIs (Apple Health, Google Health Connect minimum).
- Internal dashboard design with permission systems.
- Deployment and operations on European cloud.
- Evolutionary maintenance and deliverable technical documentation.

### 12.2 Required deliverables in the proposal

| ID | Deliverable |
|----|------------|
| E1 | Technical proposal with recommended architecture |
| E2 | Specific AI architecture (RAG, models, voice, vector, cost control) |
| E3 | Development phases with deliverables per phase |
| E4 | Per-phase time estimation |
| E5 | Cost estimation broken down (development, infrastructure, tokens/inference, voice) |
| E6 | Infrastructure cost estimation by scenario (1,000 active users: low, medium, high — source § 18.5) |
| E7 | Assigned team with roles and experience |
| E8 | Proposed tech stack with justification and portability |
| E9 | Post-launch maintenance plan (evolutionary + corrective) with severity-based SLAs and support hours |
| E10 | Security measures and test plan |
| E11 | Identified technical risks with mitigations |
| E12 | Documented delivery plan to avoid structural vendor dependency |
| E13 | **Explanatory video** (FR-702) production / integration plan: vendor's internal production, externalisation to a content partner, or player only + integration (Itabey provides the video) |
| E14 | **Recurring monthly cost** broken down by component (infrastructure, LLM, voice, vector, human support) and low/medium/high scenarios per 1,000 active users |
| E15 | **Architectural readiness document for HL7/FHIR**: how the data model can be mapped to those standards in a later phase without structural redesign |
| E16 | **Migration / exit plan** (anti vendor lock-in): how Itabey would continue operating without the vendor, with time and cost estimate |
| E17 | **Demonstration of modular architecture and tiering capability** (FR-1306, FR-1307): prior project reference or technical proof showing feature flags as a first-class architectural capability, not as an add-on |

### 12.3 Project-closure deliverables

- Full source code under Itabey's ownership.
- Comprehensive technical documentation (architecture, integrations, runbooks).
- NDA and commitment of non-reuse of project-specific components.
- Commitment not to generate derivative products based on Itabey/Asha logic.

### 12.4 Weighted evaluation criteria (proposal)

> 🏷️ **PROPOSAL — weights to validate by the CEO based on strategic priorities.**

| Criterion | Proposed weight |
|-----------|-----------------|
| HealthTech experience + GDPR | 18% |
| **Modular technical architecture with tiering capability** (FR-1306–1307, NFR-SC06–07) — decoupled, feature flags as first-class, no lock-in | **20%** |
| Conversational AI + RAG experience | 15% |
| Assigned team and experience | 12% |
| Total cost of ownership (development + infrastructure + estimated AI costs, including per-tier quotas) | 15% |
| Post-launch maintenance plan (SLAs, support, recurring costs — § 4.10) | 10% |
| Delivery plan and documentation (anti vendor lock-in, exit plan E16) | 5% |
| Documented HL7/FHIR readiness (E15) | 5% |

> **Evaluation notes:**
> - A proposal can comply with every individual FR and still **fail to meet this PRD** if it delivers monolithic architecture. The modularity/tiering criterion is **discriminating**, not cumulative.
> - "HealthTech + GDPR experience" is evaluated on verifiable references, not declarations.
> - A proposal without convincing demonstration of E17 (modular capability) is rejected for the final round, regardless of cost.

---

## Appendix

### A. Source documents

- `docs/fuentes/Documento de Requerimientos Funcionales_ Itabey _ Asha.md` (Itabey CEO, v1.0) — starting document.
- `docs/fuentes/Itabey-Pitch-Deck.pdf` — investor material.
- `docs/fuentes/Doc Pool.pdf` — additional reference.
- `docs/fuentes/P. Alex .pdf` — material related to the consultant role.
- `docs/rol/definicion-rol-consultor-tecnico.md` — consultant role scope (Alex Santolaria).
- `docs/informes/consideraciones-y-riesgos-iniciales.md` — initial risk report.

### B. Next steps

- Technical architecture design — to be produced as a sibling document once the open questions of § 11 are answered by the CEO and a vendor is selected.
- Development tickets — generated after the architecture is agreed.

### C. Scope this PRD does **not** define

- **Concrete architectural decisions** (specific stack, models, cloud provider): delegated to the vendor and to the architecture design phase.
- **Concrete visual design** (palette, typography): delegated to the UX/UI design phase based on NFR-A and source § 14.3.
- **Concrete schedule and budget**: emerge from vendor proposals.


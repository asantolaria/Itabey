# Itabey / Asha — Product Requirements Document

**Revision:** 3
**Revision date:** 2026-05-29
**Owning entity:** Polymita Systems SL
**Status:** Reference document for development proposal evaluation

> This document defines the functional scope, technical requirements, constraints and evaluation criteria for the development of the Itabey/Asha product. It serves as the basis for development vendors to prepare their proposal. Decisions marked 🛡️ **NON-NEGOTIABLE** are non-negotiable project requirements and must be respected in full in any proposal.

---

## 0. How to read this document

This PRD is governed by **three cross-cutting axes** marked on every FR/NFR:

| Axis | Values | Meaning |
|------|--------|---------|
| **Delivery phase** | Phase 1 (MVP) · Phase 2 (Evolution) | **When** the functionality is delivered. Phase 1 is the initial commercial launch; Phase 2 is the subsequent evolution with verticals and expansions. |
| **MoSCoW priority** | Must · Should · Could | **Importance within its phase**. Must = non-negotiable delivery in that phase; Should = expected delivery with some margin; Could = delivered only if scope allows. |
| **Origin restriction** | 🛡️ NON-NEGOTIABLE · (no mark) | Decisions marked non-negotiable are non-negotiable project requirements. Others are standard practice criteria. |

**Reading rule for vendors:** the combination *Phase 1 + Must* defines the minimum scope of the MVP. A proposal that fails to deliver all *Phase 1 Must* items does not meet this PRD.

---

## 1. Product vision and goals

### 1.1 Vision

**Itabey** is a digital system for **longitudinal women's health support**, focused on recording, visualisation, interpretation, and follow-up of hormonal, physical, emotional, behavioural, and contextual data.

**Asha** is the conversational engine integrated into Itabey. It interprets data entered by the user, detects patterns, generates non-diagnostic hypotheses, offers contextual support, and recommends clinically validated educational content.

The product's core value **does not lie in data capture** but in its capacity for interpretation, learning, and continuous longitudinal support. The versioned biomedical knowledge base and the RAG engine on top of it constitute, alongside the user experience, the **defensible asset** of the product.

### 1.2 Goals

| ID | Goal | Measured via |
|----|------|--------------|
| G1 | Support the user in self-knowledge of her cyclical health through longitudinal data | D90 retention, registration frequency, NPS |
| G2 | Reduce friction in data entry through natural voice and wearable/health-app integration | % voice entries, % users with connected wearable |
| G3 | Generate structured reports that facilitate medical consultations | % users who generate a report within 90 days, satisfaction of receiving professionals |
| G4 | Build a clinically validated, versioned biomedical knowledge base as the central asset | Volume of validated capsules, mean time to validation |
| G5 | Enable Asha as a decoupled, future-licensable engine via API/white-label | Public API coverage, third-party integration time |
| G6 | Comply with GDPR (Art. 9) and embed Privacy/Security by design from the architecture onward | Successful external audit, zero data breach incidents |
| G7 | Position the product in Spanish-speaking markets with cultural sensitivity (Spain + LATAM + Hispanic communities in the US) | Geographic distribution of signups, country-level adoption, qualitative satisfaction |

### 1.3 Non-goals

| ID | Non-goal | Reason |
|----|----------|--------|
| NG1 | 🛡️ **Clinical diagnosis** | Asha does not diagnose, prescribe, or replace medical consultation |
| NG2 | CE marking / medical device (MDR) classification in MVP | Out of scope for time and budget; architecture must allow it later |
| NG3 | HL7/FHIR compliance in MVP | Out of MVP. **It is required** that the architecture allow later mapping without structural redesign — see § 4.10, NFR-M, E15 in § 11.2 |
| NG4 | Women's sports vertical in MVP | Deferred to Phase 2; architecture must reserve integration surface |
| NG5 | White-label / API licensing of Asha in MVP | Deferred to Phase 2; architecture must allow it from day 1 |
| NG6 | 🛡️ **Sale of personal data or commercial exploitation of individual information** | Ethical/GDPR commitment of the product |
| NG7 | Advanced wearables (Whoop, full Oura, Garmin) in MVP | Initial integrations: Apple Health + Google Health Connect |
| NG8 | Active scientific research with institutions in MVP | Architecture prepared (data philanthropy model), execution deferred to Phase 2 |
| NG9 | Male adaptation of the product in MVP | Deferred to Phase 2; architecture must allow it without redesign |
| NG10 | Specific tools for professional patient-management profiles in MVP | Deferred to Phase 2; the role and permission system must architecturally enable them from the start |

### 1.4 Product phase structure

> The product is split into **two phases**. Phase 1 (MVP) is the initial commercial launch. Phase 2 (Evolution) groups all subsequent expansions. The MVP launches commercially for B2C **and** initial B2B clients, but as a "solid, coherent and scalable core", not as a giant system.

#### 1.4.0 MVP focus

> **MVP core pillars.** The MVP focuses on doing the following extremely well — the basis on which the product's value proposition is validated:
>
> - **Asha** — the conversational engine with RAG architecture (FR-201 to 209)
> - **Tracking** — structured user data entry, manual and by voice (FR-101 to 105)
> - **Insights** — basic longitudinal pattern detection and self-knowledge panel in its initial version (FR-302 basic)
> - **Internal calendar** — canonical view of the user's cyclical information (FR-303)
> - **UX** — intuitive, fluid, accessible user experience, with thoughtful onboarding (FR-701, FR-702) and cross-cutting modes (neurodivergent mode, crisis mode — NFR-A)
>
> **Functionality explicitly out of MVP** — **but architecturally prepared from day 1 for incorporation in Phase 2 without structural redesign**:
>
> | Functionality | FR | Why out of MVP |
> |---|---|---|
> | Moderated community / forum and its moderation panel | FR-501, FR-1004 | High complexity and cost; not critical for validating the core |
> | Shared panel (partner, mother, daughter, caregiver) | FR-305 | Expansion functionality, not core validation |
> | Body map / 3D illustrations | FR-304 | Significant visual investment; basic structured logging is enough to validate |
>
> This decision reduces MVP complexity, time, and cost. The modular architectural capability (FR-1306, FR-1307, NFR-SC06) guarantees that these functionalities can be incorporated in Phase 2 by activation, without touching the core system and without data loss for existing users.

#### 1.4.1 Scope by phase

| Phase | Horizon | Scope |
|-------|---------|-------|
| **Phase 1 — MVP** | Commercial launch | Full B2C (registration, Asha with RAG, internal calendar, main panel, basic reports, onboarding, full privacy and security, minimal dashboards, voice, initial health integrations, risk detection) **+** B2B core (single account, access modes, corporate linkage, B2B privacy, aggregate analytics dashboard for client organisation) **+** architectural capability for tiering and modularity |
| **Phase 2 — Evolution** | Post-launch | Full B2B (enterprise SSO, advanced corporate dashboard, contracts, SLA support), full moderated community, advanced self-knowledge panel, body map, shared panel, full internal dashboards, bidirectional sync with external calendars, advanced integrations (deep links, third-party APIs, app referrals), reports for professionals, women's sports vertical, male adaptation, professional patient-management profile, API licensing and white-label of Asha, HL7/FHIR mapping, scientific research with institutions, international expansion beyond Spanish-speaking markets |

#### 1.4.2 Functionality matrix by area and phase

> This is the **canonical table** the development team should use to plan deliverables. Each cell cites the applicable FRs.

| Functional area | Phase 1 — MVP | Phase 2 — Evolution |
|-----------------|---------------|---------------------|
| Data capture | FR-101, FR-102, FR-103 *(basic)*, FR-104 *(Apple Health + Google Health Connect)*, FR-105 | FR-103 *(full voice-only mode)*, FR-106 *(bidirectional calendar sync)*, FR-104 *(advanced wearables)* |
| Asha conversational | FR-201, FR-202, FR-203, FR-204, FR-205, FR-206, FR-207, FR-208, FR-209 | FR-210 *(public API)*, expanded RAG layers, white-label |
| User panels | FR-301, FR-303, FR-302 *(basic version)* | FR-302 *(advanced)*, FR-304, FR-305 |
| Reports | FR-401 | FR-402, FR-403 |
| Community and content | FR-502 *(reduced initial catalogue)* | FR-501, FR-503 |
| Personalisation | FR-601, FR-602 | FR-603 |
| Onboarding and help | FR-701, FR-702 *(explanatory video)* | — |
| Notifications | FR-801 *(basic)* | FR-801 *(complete)* |
| Privacy and data | FR-901, FR-902, FR-903, FR-904, FR-905 | — |
| Internal dashboards | FR-1001 *(Super Admin with MVP operational view)*, FR-1002 *(partial)* | FR-1001 *(complete)*, FR-1002 *(complete)*, FR-1003, FR-1004, FR-1005 |
| Health integrations | FR-1101 *(Apple Health + Google Health Connect)* | FR-1101 *(Oura, Whoop, Fitbit, Garmin)*, HL7/FHIR mapping |
| Calendar integrations | FR-1102 *(import FR-105)* | FR-1102 *(bidirectional sync FR-106)* |
| External apps and deep links | FR-1110 *(architecture prepared, not operational)*, FR-1113 *(open architecture)* | FR-1111 *(Asha app recommendations)*, FR-1112 *(deep links and install)*, FR-1114 *(third-party APIs)* |
| Risk detection | FR-1201 | — |
| Account management and tiers | FR-1301, FR-1302 *(free + individual + basic B2B)*, FR-1303 *(migration)*, FR-1304 *(B2B privacy)*, FR-1306 *(tiering capability)*, FR-1307 *(feature flags)* | FR-1302 *(full B2B)*, FR-1305 *(professional manager)*, FR-1306 *(operational tiers)* |

> **Proposal evaluation rule:** Vendor proposals must present **a Phase 1 scope coherent with this table**. A proposal that mixes Phase 1 and Phase 2 without explicit distinction must be corrected before comparing costs and timelines.

### 1.5 Depth tier model and strategic modularity

> **First-class architectural commitment.** The system **must be born modular** — capable of supporting different levels of depth and access from day 1, even though externally it feels like a single coherent product. This section elevates functional modularity to the rank of Privacy by design and Security by design principles.

#### 1.5.1 Why this matters

Itabey operates in a hybrid B2C + B2B market with fundamentally different needs:

- **Corporate client (B2B):** buys **wellbeing, prevention, engagement** for employees. Requires a solid, easy-to-deploy tool with predictable operating cost. **Does not** need the full longitudinal introspective depth of the product.
- **Individual user (B2C):** seeks **deep self-knowledge, personalisation, longitudinal support, pattern analysis, contextual memory**. She is the *power user* with the highest LTV potential.

If the system delivers all advanced capabilities to B2B from the start, the risks are material: high-volume contracts at low prices against rising infrastructure/AI costs, *power users* with no natural upgrade path, eroded margins, loss of future pricing flexibility.

If the system **is born modular**, the organisation gains: a powerful corporate experience without runaway structural costs, B2B as a low-CAC mass acquisition channel, natural upgrade paths to premium tiers for individuals, higher LTV/margin per user, the ability to adapt plans and verticals without rebuilding the product.

#### 1.5.2 What this requires of the system

The PRD **does not prescribe** which features will go in which tier — that decision is deferred until real usage data is available. What is required is the **architectural capability**:

1. **Activation/deactivation of features by user, cohort, or tier** without code changes (feature flags as a first-class capability — FR-1307).
2. **Asha depth layers** parameterisable: long-term memory depth, number of detected patterns, insight frequency, type of personalisation available — all configurable per tier without redesign (FR-1306).
3. **Resource consumption tiers**: configurable quotas per tier on LLM calls, vector storage, inference tokens, voice processing. No tier consumes unlimited resources without a cap.
4. **Modular permissions** by feature and by person, not by monolithic role.
5. **Vertical adaptation** (sports, professional profile, male adaptation, etc.) as activation of modules over the common base.

#### 1.5.3 What is not decided here

- Which exact features go in which tier (post-MVP decision, based on real usage signal).
- Commercial tier names (marketing decision).
- Tier pricing.
- Which tier B2B client employees receive (per-contract decision).

> **Proposal evaluation rule:** A vendor proposal that delivers monolithic architecture with fixed-role permissions **does not meet** this PRD, even if it complies with every individual FR. Modular tiering capability is evaluated explicitly — see § 11.4.

### 1.6 Ecosystem and owning entity

| Element | Description |
|---------|-------------|
| **Polymita Systems SL** | Owning entity of the project. Business and technological structure that supports the ecosystem. Holder of all intellectual property derived from the project. |
| **Itabey** | Main project name and platform name. Encompasses the app, the podcast, and future development lines. |
| **Asha** | Conversational engine and artificial intelligence of the ecosystem. Decoupled from Itabey via API from day 1; licensable to third parties as an independent product in Phase 2. |

Ownership of **all** code, architecture, documentation, flows, functional design, product logic, configurations, models, prompts, knowledge bases, RAG configurations, embeddings, derived weights, interfaces, integrations and deliverables corresponds entirely to Polymita Systems SL. Any external vendor cedes these rights as a contractual condition.

---

## 2. Users and personas

### 2.1 Primary personas (end users — B2C)

#### P1 — **Lara**, the curious self-learner (28–40)

- **Role:** Professional woman, no diagnosed condition.
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

> **Note:** Sara consumes the MVP through habits, energy, and general correlations. The dedicated sports vertical is Phase 2.

### 2.2 Secondary persona (B2C)

#### P4 — **Ana**, the shared person (mother, daughter, partner, professional caregiver)

- **Role:** Receives partial access to a primary user's profile via the shared panel (FR-305, Phase 2).
- **Goal:** Support/care without invading privacy.
- **JTBD:** *"Stay aware of [daughter/partner/mother] within the limits she allows me."*
- **Importance:** Retention lever and word-of-mouth acquisition vector.

### 2.3 Corporate persona (B2B client)

#### P5 — **Corporate Client** (company, insurer, mutual, healthcare system)

- **Role:** Organisation that funds Itabey/Asha access for its employees or insured as a wellbeing, prevention, or women's health benefit.
- **Goal:** Reduce absenteeism, improve engagement, offer a differential benefit, manage predictable cost.
- **JTBD:** *"I want to offer a solid health and wellbeing tool to my employees without assuming clinical responsibility or accessing their individual data."*
- **Access:** Linkage via company code, invitation, or enterprise SSO (Phase 2 complete). Own aggregate analytics dashboard (overall usage, aggregate satisfaction, anonymous cohorts), without access to individual data or conversations (FR-1304).
- **Restrictions:** **Cannot** inherit accounts, **does not** access personal data or conversations, **does not** direct clinical content, **has no** operational control of the system.
- **Commercial importance:** Low-CAC mass acquisition channel; predictable recurring revenue.

### 2.4 Internal personas (system operation)

> These profiles operate **inside** the Polymita Systems team or as clinical collaborators. They are not end users. Each profile has its own dashboard, permissions, and specific restrictions.

#### PI1 — **Super Admin / Founder**

- **Role:** Global supervision and control of the ecosystem at strategic, operational, technical, functional, and content levels.
- **Goal:** Integral management of the platform, supervision of Asha's behaviour, coordination of biomedical and educational content, system monitoring, and global product administration.
- **Dashboard:** FR-1001 (includes superset of the other dashboards).
- **Capabilities:**
  - Global system supervision.
  - Business metrics (retention, churn, DAU/WAU/MAU, cohorts).
  - Engagement and aggregate behaviour metrics.
  - Overall technical status and incidents.
  - Integration supervision.
  - Permission and role management.
  - Feature flag and modular activation management (FR-1307).
  - Tier and resource consumption management (FR-1306).
  - Asha performance and quality monitoring.
  - Review of anonymised or reported conversations (quality control).
  - Edit and update of Asha's content and knowledge.
  - Management and versioning of educational capsules.
  - Full moderation of community and forum.
  - Audit and traceability tools.
  - Progressive deployment and functional rollback.
- **Restrictions:**
  - Access to individual sensitive data and full private conversations limited to specific contexts (support, security, critical incidents, moderation, or quality review).
  - Information preferentially displayed in aggregated, anonymised, or pseudonymised formats.
  - All administrative actions and sensitive reviews recorded via internal audit (NFR-S06).

#### PI2 — **Multidisciplinary clinical team**

- **Role:** Initial team of 5 clinical/health profiles (family medicine, gynaecology, mental health, endocrinology, anaesthesia and pain; progressively expandable).
- **Goal:** Biomedical validation, definition of general clinical criteria, protocol review, educational content validation, conceptual supervision of the system.
- **Dashboard:** FR-1002.
- **Capabilities:** Entering structured clinical knowledge, validating biomedical content, defining general criteria, reviewing correlations, versioning clinical knowledge, approving educational capsules, defining the hard-stop catalogue.
- **Restrictions:** No access to individual personal data, no access to private conversations, no access to business metrics, no operational control of the system.

#### PI3 — **Community and forum moderation**

- **Role:** Supervision, moderation, and maintenance of the community and social space (Phase 2).
- **Goal:** Ensure a safe, respectful environment aligned with community norms; reduce spam, misinformation, conflicts, and disallowed sensitive content.
- **Dashboard:** FR-1004.
- **Capabilities:** Moderation of posts and comments, management of reported content, anti-spam tools, detection and review of sensitive content, temporary or permanent blocking of accounts, category management, community incident supervision, aggregate metrics, review of AI moderation alerts, internal escalation of serious incidents.
- **Restrictions:** No full access to business metrics, no access to clinical backend, no access to private Asha conversations, no access to individual sensitive data outside moderated content.

#### PI4 — **Analytics and data supervision**

- **Role:** Longitudinal and population analytical supervision of aggregate system behaviour.
- **Goal:** Analyse usage patterns, longitudinal metrics, aggregate behaviour, functional performance, and global platform evolution to improve product, experience, and collective learning.
- **Dashboard:** FR-1003.
- **Capabilities:** Aggregate analytical dashboards, cohorts and retention, usage and engagement metrics, anonymised longitudinal trends, data quality and consistency, feature performance, aggregate Asha metrics, emerging pattern detection, authorised anonymised dataset export, performance supervision by tiers and cohorts.
- **Restrictions:** No access to personally identifiable data, no free access to individual conversations, no global administrative permissions, no editing of biomedical content or critical configuration.

#### PI5 — **Senior technical supervision**

- **Role:** Technical supervision, stability, and structural maintenance of the system.
- **Goal:** Monitor infrastructure, stability, security, and overall technical performance of Itabey/Asha.
- **Dashboard:** FR-1005.
- **Capabilities:** Overall infrastructure status, monitoring of APIs and integrations, backend/frontend performance, technical logs and critical alerts, error and incident supervision, deployment status, observability, security and anomaly supervision, technical consumption metrics, supervision of internal pipelines and services.
- **Restrictions:** No free access to individual clinical data, no access to private conversations, no strategic product control, no modification of biomedical content, no financial or business access except necessary technical metrics.

### 2.5 Cross-cutting notes

- **Neurodivergent mode:** Not a persona, a **cross-cutting usage mode** that any persona (P1–P4) can activate. Treated as a non-optional UX requirement for MVP (NFR-A04).
- **Professional patient-management profile (Phase 2):** Professionals (clinicians, social workers, health coaches) who manage several users/patients with their explicit consent. **Not** part of the MVP. Distinct from PI2 (internal clinical team that validates generic knowledge); see FR-1305.

---

## 3. Functional requirements

> **ID convention:** Groups are numbered by hundreds (FR-1xx, FR-2xx, …) by functional area. Each FR specifies MoSCoW priority, delivery phase, and testable acceptance criteria.

### 3.1 Data capture (FR-1xx)

#### FR-101 — Manual user data entry
- **Phase:** 1 (MVP) — **Priority:** Must
- **Description:** The user can manually enter data on cycle, symptoms, emotions, habits, sleep, and events.
- **Trigger:** Explicit user action from main panel or calendar.
- **Expected outcome:** Data persisted, reflected in panel and calendar in < 2 seconds.
- **Acceptance criteria:**
  - Any entry persists offline and syncs upon connectivity recovery (offline-first).
  - Data is editable and deletable by the user without restrictions.
  - Each data category has a structured schema (no opaque free text).

#### FR-102 — Structured voice-based entry
- **Phase:** 1 (MVP) — **Priority:** Must
- **Description:** The user can update structured data through natural language by voice.
- **Trigger:** Wake-word activation or button.
- **Examples:** *"Got my period today"*, *"My lower back hurts"*, *"I slept poorly"*, *"I'm very irritable"*.
- **Expected outcome:** The system interprets the phrase, extracts intent and entity, updates the corresponding structured data, and shows visual confirmation.
- **Acceptance criteria:**
  - Correct interpretation rate ≥ 90% on a Spanish and English test corpus.
  - Every interpretation is confirmable/correctable by the user before persistence.
  - Voice entry covers at minimum: cycle, localised pain, mood, sleep, events.

#### FR-103 — Voice-only mode
- **Phase:** 1 (MVP, basic) / 2 (Evolution, full navigation) — **Priority:** Should
- **Description:** The application is navigable and operable using voice only.
- **MVP acceptance criteria:**
  - Core functionality (entry, Asha consultation, basic report generation) is accessible without touching the screen.
  - Compatibility with native screen readers (VoiceOver, TalkBack).

#### FR-104 — Wearable import
- **Phase:** 1 (MVP — Apple Health + Google Health Connect) / 2 (Evolution — Oura, Whoop, Fitbit, Garmin, equivalents) — **Priority:** Must (MVP) / Should (Evolution)
- **Description:** Import biometric data from supported wearables.
- **Supported variables:** sleep, activity, heart rate, temperature, HRV, recovery, fatigue, training.
- **Acceptance criteria:**
  - User-revocable connection at any time.
  - Imported data clearly separated from manual data (source traceability).
  - Clear reconciliation when manual and wearable data exist for the same event.

#### FR-105 — External calendar event import
- **Phase:** 1 (MVP) — **Priority:** Should
- **Description:** One-way import of relevant events from Google Calendar and Apple Calendar (medical appointments, life events, travel) into the internal calendar panel (FR-303).
- **Acceptance criteria:**
  - User-driven activation, granular control of which calendars are read.
  - Configurable obfuscation of sensitive titles/descriptions before import.
  - Immediate deactivation; imported events removed on request.

#### FR-106 — Bidirectional external calendar sync
- **Phase:** 2 (Evolution) — **Priority:** Should
- **Description:** Bidirectional sync with Google Calendar and Apple Calendar that **publishes the cycle phase and selected relevant events** from the internal calendar to the user's external calendar.
- **Acceptance criteria:**
  - **Configurable visualisation** in the external calendar: the user chooses among full invisibility, small discreet daily icon, colour code, text label, or combinations.
  - Sync of cycle phases (menstruation, estimated ovulation, estimated fertility, lunar phase if active) and, optionally, selected soft reminders.
  - **Privacy by default:** no sync at start — explicit, reversible opt-in.
  - **No** sensitive data is exported (symptoms, mood, Asha conversations) under any circumstances.
  - Immediate deactivation removes all exported events without retention.
  - Compatibility with shared calendars: the user controls whether exported events are visible to third parties sharing her calendar.

### 3.2 Asha conversational engine (FR-2xx)

#### FR-201 — Text conversation
- **Phase:** 1 (MVP) — **Priority:** Must
- **Description:** Asha responds to natural-language text queries.
- **Acceptance criteria:**
  - Response in < 5 s (P95) for standard queries; < 10 s with deep RAG.
  - Each response complies with the structure in FR-205.

#### FR-202 — Voice conversation
- **Phase:** 1 (MVP) — **Priority:** Must
- **Description:** Asha responds in voice with configurable voice, accent, speed, and tone.
- **Acceptance criteria:**
  - Voice-to-voice latency < 3 s (P95) for short responses.
  - Voice selectable by the user from a configurable catalogue.

#### FR-203 — RAG architecture
- **Phase:** 1 (MVP) — **Priority:** 🛡️ **NON-NEGOTIABLE — Must**
- **Description:** Every Asha response relies on a controlled, validated, versioned knowledge base.
- **Acceptance criteria:**
  - 100% of biomedical-content responses internally cite the RAG source used (traceability).
  - Corpus version changes are auditable and reversible.
  - Hallucination control: if retrieval confidence is low, Asha downgrades the response to "I have no validated information on this" rather than generating freely.

#### FR-204 — Differentiated memory (short / long term)
- **Phase:** 1 (MVP) — **Priority:** Must
- **Description:** Asha maintains short-term memory (current conversation) and long-term memory (patterns, preferences, useful conclusions).
- **Acceptance criteria:**
  - Full conversations are **not** stored as permanent memory by default.
  - Long-term memory is **selective** (patterns, relevant data, conclusions).
  - The user can inspect, edit, and delete long-term memory.

#### FR-205 — Asha response structure
- **Phase:** 1 (MVP) — **Priority:** Must
- **Description:** Responses may include the following blocks:
  - Main answer
  - Contextual explanation
  - Practical suggestion
  - Optional educational capsule
  - Optional fact/curiosity
  - Content recommendation (including external apps — see FR-1111, Phase 2)
  - Feedback button (FR-206)
  - Visible warning (FR-207)
- **Acceptance criteria:**
  - The "visible warning" block is **mandatory** in responses with health content.

#### FR-206 — User feedback per response
- **Phase:** 1 (MVP) — **Priority:** Must
- **Description:** Each Asha response allows quick feedback: like / dislike / it helped / it didn't help / report / ask for simpler explanation / ask for more depth.
- **Acceptance criteria:**
  - Feedback feeds internal quality metrics **without exposing individual conversations**.
  - Feedback is reviewable by the administration team in aggregate.

#### FR-207 — Visible, persistent disclaimers
- **Phase:** 1 (MVP) — **Priority:** 🛡️ **NON-NEGOTIABLE — Must**
- **Description:** The interface visibly and persistently shows:
  - "Asha does not provide diagnoses."
  - "Asha does not replace a healthcare professional."
  - "Asha may make mistakes."
  - "For severe symptoms or medical doubts, consult a professional."
- **Acceptance criteria:**
  - Disclaimers present at: first response of each session, sensitive conversations, generated reports, health-related recommendations.

#### FR-208 — Hard-stop protocol
- **Phase:** 1 (MVP) — **Priority:** 🛡️ **NON-NEGOTIABLE — Must**
- **Description:** Faced with severe risk signals (self-harm, intense emotional crisis, possible medical emergency), Asha **suspends generative response** and activates a predefined response oriented toward professional referral or emergency services.
- **Acceptance criteria:**
  - 100% of detected cases activate the predefined response (no free generation).
  - Each activation is logged for clinical audit with metadata: timestamp, signal type, resource offered.
  - The catalogue of signals and predefined responses is validated and versioned by the clinical team (FR-1002).

#### FR-209 — Generation of non-diagnostic hypotheses
- **Phase:** 1 (MVP) — **Priority:** Must
- **Description:** Asha may generate non-clinical hypotheses, detect patterns, suggest observations, recommend professional consultation.
- **Restriction:** **Never** issues a diagnosis, **never** indicates personalised medical treatment.

#### FR-210 — Public Asha API
- **Phase:** 1 (MVP — stable internal API) / 2 (Evolution — public exposure for licensing) — **Priority:** Should
- **Description:** Asha exposes a stable internal API that will, in the future, be exposed publicly for licensing.
- **Acceptance criteria:**
  - Asha is callable from outside the Itabey frontend via a documented API.
  - Semantic API versioning.
  - Coupling between Asha and Itabey occurs exclusively via this API (no shortcuts).

### 3.3 User panels (FR-3xx)

#### FR-301 — Main panel
- **Phase:** 1 (MVP) — **Priority:** Must
- **Content:** Current state, contextual summary, quick access, Asha suggestions, upcoming relevant events, cycle phase, soft reminders, quick voice/text entry.

#### FR-302 — Self-knowledge panel
- **Phase:** 1 (MVP, basic version) / 2 (Evolution, advanced version) — **Priority:** Should (MVP) / Must (Evolution)
- **MVP content:** Basic detected patterns, longitudinal evolution, simple time-series charts.
- **Evolution content:** Comparisons across cycles and periods, improvement/worsening metrics, recommendation history, personal and dynamically suggested goals, completion tracking, Asha-generated insights.

#### FR-303 — Internal calendar panel
- **Phase:** 1 (MVP) — **Priority:** Must
- **Description:** Itabey's own calendar. **Canonical view** of the user's cyclical information inside the app.
- **Content:** Hormonal cycle, menstruation, estimated ovulation, estimated fertility, energy states, lunar phase, manual events, relevant symptoms, soft predictions, configuration of visible elements.
- **Explicit distinction:** Sync with external calendars (Google/Apple) is not part of this FR. It is specified separately in FR-105 (event import, MVP) and FR-106 (bidirectional sync, Phase 2).

#### FR-304 — Body panel
- **Phase:** 2 (Evolution) — **Priority:** Should
- **Content:** Interactive body map (3D or pseudo-3D), zone selection, pain/symptom logging by zone, temporal evolution, educational explanation, association with cycle/habits/sleep/stress.

#### FR-305 — Shared panel
- **Phase:** 2 (Evolution) — **Priority:** Should
- **Description:** The user can share information granularly and temporarily with: partner, mother/daughter, healthcare professional, authorised carer.
- **Acceptance criteria:**
  - The user controls **what** she shares, **for how long**, and **with whom**.
  - Immediate revocation without consequences for the data.

### 3.4 Reports and export (FR-4xx)

#### FR-401 — Reports for the user
- **Phase:** 1 (MVP) — **Priority:** Must
- **Content:** Longitudinal evolution, symptoms, cycle, emotional state, patterns, goals, recommendations, comparatives, charts.
- **Formats:** PDF minimum in MVP.

#### FR-402 — Reports for professionals
- **Phase:** 2 (Evolution) — **Priority:** Should
- **Content:** Structured clinical summary, symptoms by period, observed correlations, cycle evolution, relevant entries, history, life events, preparation for medical consultation.
- **Acceptance criteria:**
  - Format intended for printing and delivery in consultation (no professional login required).
  - Clear identification that the document is generated by Itabey and does not constitute a diagnosis.

#### FR-403 — Reports from Asha conversation
- **Phase:** 2 (Evolution) — **Priority:** Should
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
- **Phase:** 2 (Evolution) — **Priority:** Should
- **Functionality:** Posts, comments, optional anonymity, categories, reports, manual + AI-assisted moderation, sensitive-content filtering, user blocking, moderation history, aggregated recommendations.
- **Restrictions:**
  - Asha **does not** expose individual data when recommending community content.
  - Proactive detection and blocking of spam, misinformation, and conflict.

#### FR-502 — Educational content capsules
- **Phase:** 1 (MVP, reduced initial catalogue) / 2 (Evolution, expanded catalogue) — **Priority:** Must
- **Description:** Information capsules by symptom, cycle phase, emotional state, need.
- **Acceptance criteria:**
  - All biomedical content is validated and versioned by the clinical team before publication.
  - Capsules feed Asha's RAG base.

#### FR-503 — Podcast recommendations
- **Phase:** 2 (Evolution) — **Priority:** Could
- **Description:** Recommendation of project podcast episodes and fragments; automatic transcription; indexing.

### 3.6 Personalisation (FR-6xx)

#### FR-601 — Asha personalisation
- **Phase:** 1 (MVP) — **Priority:** Must
- **Configurable:** Tone (direct, empathetic, technical, realistic, soft, structured), personality, depth level, style, voice, accent, speed, preferred focus.

#### FR-602 — Language levels
- **Phase:** 1 (MVP) — **Priority:** Must
- **Levels:** Simple, technical, advanced.
- **Acceptance criteria:**
  - User changes level at any time, in any conversation.
  - Educational capsules exist at least in Simple and Technical levels.

#### FR-603 — Activatable focus modules
- **Phase:** 2 (Evolution) — **Priority:** Should
- **Focuses:** Scientific, integrative, emotional, wellbeing, spiritual, complementary.
- **Restriction:** Complementary focuses are presented as **optional layers of observation**, neither replacing medicine nor positioned at the same evidence level.

### 3.7 Onboarding (FR-7xx)

#### FR-701 — Progressive conversational onboarding
- **Phase:** 1 (MVP) — **Priority:** Must
- **Steps:** Profile creation, initial configuration, focus selection, Asha tone selection, language level selection, privacy explanation, consent, introduction to functioning, progressive feature activation.
- **Acceptance criteria:**
  - No onboarding step overwhelms the user with > 3 simultaneous decisions.
  - Consent is granular (no global checkbox) and revocable.

#### FR-702 — In-product explanatory video
- **Phase:** 1 (MVP) — **Priority:** Should
- **Description:** Short video (< 3 min) explaining how the app works, accessible from onboarding (skippable) and from a permanent help menu (re-watchable).
- **Acceptance criteria:**
  - Available at least in Spanish and English (NFR-I01).
  - Closed captions (CC) toggleable by default.
  - Skippable at any time during onboarding without flow penalty.
  - Re-watchable from help menu → "How does Itabey work?".
  - Plays offline if cached.
- **Scope note:** This FR covers the player, in-product integration, and accessibility. **Production of video content** (script, voiceover, animation) is the responsibility of the development vendor or a contracted content vendor — to be made explicit in budget (E13) if delegated.

### 3.8 Notifications (FR-8xx)

#### FR-801 — Soft notifications system
- **Phase:** 1 (MVP, basic set) / 2 (Evolution, full set) — **Priority:** Should
- **MVP types:** Registration reminders, cycle alerts, incomplete-record alerts.
- **Evolution types:** Contextual alerts, proactive suggestions, anticipatory preparation, goal tracking, content recommendations.
- **Acceptance criteria:**
  - User adjusts frequency, type, and intervention level.
  - Non-invasive notifications by default (opt-in for specific types).

### 3.9 Privacy and data control (FR-9xx)

#### FR-901 — Visibility of stored data
- **Phase:** 1 (MVP) — **Priority:** 🛡️ **NON-NEGOTIABLE — Must**
- The user can see at any time which data is stored about her.

#### FR-902 — Data export
- **Phase:** 1 (MVP) — **Priority:** 🛡️ **NON-NEGOTIABLE — Must**
- Full export in structured format (JSON + summary PDF).

#### FR-903 — Data deletion / right to be forgotten
- **Phase:** 1 (MVP) — **Priority:** 🛡️ **NON-NEGOTIABLE — Must**
- Total deletion with explicit confirmation; technical traceability of deletion for audit without retaining content.

#### FR-904 — Granular consent control
- **Phase:** 1 (MVP) — **Priority:** 🛡️ **NON-NEGOTIABLE — Must**
- Independent activation/deactivation for: Asha memory, aggregate use for research, integrations (health, calendar, external apps), sharing (shared panel), specific notifications, external app recommendations (FR-1111).

#### FR-905 — Pause tracking
- **Phase:** 1 (MVP) — **Priority:** Must
- The user can pause tracking (without deletion) and resume later.

### 3.10 Internal dashboards (FR-10xx)

> Each dashboard corresponds to an internal persona (§ 2.4). Permissions and restrictions for each are detailed there.

#### FR-1001 — Super Admin / Founder dashboard
- **Phase:** 1 (MVP, minimal operational view) / 2 (Evolution, full view) — **Priority:** Must (MVP) / Should (Evolution)
- **Persona:** PI1.
- **MVP minimal view:** Total users, MAU/WAU/DAU, aggregate retention, critical incidents, overall technical status, Asha moderation alerts, feature flag management (FR-1307), tier management (FR-1306).
- **Evolution full view:** Superset of FR-1002 to FR-1005 dashboards, advanced content management, detailed metrics, full audit tools, progressive deployment, and rollback.

#### FR-1002 — Clinical dashboard
- **Phase:** 1 (MVP, partial view) / 2 (Evolution, full view) — **Priority:** Must (MVP) / Should (Evolution)
- **Persona:** PI2.
- **Allows:** Entering structured clinical knowledge, validating biomedical content, approving educational capsules, defining general criteria, validating correlations, proposing clinical variables, defining referral criteria (hard-stop catalogue), reviewing protocols, versioning knowledge.
- **Restrictions:** No access to individual personal data, no access to individual conversations, no access to business metrics, no operational control of the system, no ability to modify product or global configuration.

#### FR-1003 — Analytics dashboard
- **Phase:** 2 (Evolution) — **Priority:** Should
- **Persona:** PI4.
- **Content:** Usage behaviour, cohorts, retention, population patterns, longitudinal trends, data quality, Asha performance, educational content impact, hypothesis validation, anonymised dataset export with prior consent.

#### FR-1004 — Community moderation dashboard
- **Phase:** 2 (Evolution, coupled to FR-501) — **Priority:** Should
- **Persona:** PI3.
- **Content:** Post and comment management, reported content, manual + AI-assisted moderation, sensitive-content detection, temporary user blocks, anti-spam tools, history, metrics, conflict alerts.

#### FR-1005 — Technical supervision panel
- **Phase:** 2 (Evolution) — **Priority:** Should
- **Persona:** PI5.
- **Access:** Read-only for senior technical supervision.
- **Content:** Overall system status, availability, performance, critical incidents, integration status, aggregate technical metrics, general Asha usage, relevant alerts.
- **Restrictions:** No code edits, no structural changes, no operational control, no access to individual personal data, no access to conversations.

#### FR-1006 — Corporate dashboard (B2B client)
- **Phase:** 1 (MVP, minimal aggregate view) / 2 (Evolution, full view) — **Priority:** Should (MVP) / Must (Evolution)
- **Persona:** P5 (corporate client).
- **MVP content:** Anonymous aggregate metrics — total active employees (≥ 10 to prevent re-identification), aggregate satisfaction, global adoption rate.
- **Evolution content:** Anonymous cohorts by department (where cohort size allows), aggregate temporal trends, reported benefits, aggregate wellbeing metrics (average energy, aggregate stress levels, etc.).
- **Restrictions (FR-1304):** **Never** access to individual data, conversations, identities, or metrics enabling re-identification.

### 3.11 External integrations (FR-11xx)

#### 3.11.1 Health platforms and wearables

##### FR-1101 — Health platform integration
- **Phase:** 1 (MVP — Apple Health + Google Health Connect) / 2 (Evolution — Oura, Whoop, Fitbit, Garmin) — **Priority:** Must (MVP) / Should (Evolution)
- **MVP variables:** Sleep, activity, heart rate, temperature, HRV.

#### 3.11.2 External calendars

##### FR-1102 — External calendar integration (umbrella)
- **Phase:** 1 (MVP, via FR-105 import) / 2 (Evolution, via FR-106 bidirectional sync) — **Priority:** Should
- **Integrations:** Google Calendar, Apple Calendar (official APIs and, where applicable, CalDAV).
- **Cross-cutting criteria:** User-driven activation, granular configuration, immediate deactivation, privacy by default.

#### 3.11.3 External apps and deep links

> The system must be able to recommend external apps (sleep, meditation, nutrition, training, fertility, neurodivergence, etc.) when they add value to the user, with explicit consent and a fluid experience. **The architecture must be prepared from MVP**; operational activation is Phase 2.

##### FR-1110 — Architecture prepared for deep links and external integrations
- **Phase:** 1 (MVP, architecture prepared) — **Priority:** Must
- **Description:** The system supports, from day 1, opening external applications installed on the device via deep links and redirecting to the app store if the app is not installed.
- **Acceptance criteria:**
  - The mobile frontend architecture includes native handling of deep links (iOS Universal Links + Android App Links).
  - A "external integrations" module exists in the code, prepared for activation (FR-1111, FR-1112) without structural redesign.
  - No deep link is activated in MVP — only the technical capability is in place.

##### FR-1111 — External app recommendations by Asha
- **Phase:** 2 (Evolution) — **Priority:** Should
- **Description:** Asha may recommend specific external applications based on context, need, or detected pattern. Examples: sleep apps, meditation, nutrition, training, fertility, neurodivergence support, etc.
- **Critical restrictions:**
  - **Prior consent:** External app recommendations require explicit opt-in in FR-904 (granular, revocable).
  - **Not clinical advice:** Every recommendation carries the disclaimer "This is a suggestion based on aggregate patterns and does not constitute medical or clinical advice" (reinforcing FR-207).
  - **No hidden monetary affiliation:** If a commercial agreement exists with an external provider, it must be **transparently disclosed** in the interface when showing the recommendation. If no agreement, it is also indicated as a free editorial recommendation.
  - **Curated catalogue:** The catalogue of recommendable apps is validated by the clinical team (PI2) or product lead (PI1) before being added to the system. Free LLM-driven recommendations are not allowed.
- **Acceptance criteria:**
  - Each recommendation includes: app name, brief reason, disclaimer, transparency indicator (affiliation or not), "open/download" button, "not interested" button, "no more recommendations of this type" button.
  - User feedback on recommendations feeds internal metrics without exposing her profile to third parties.

##### FR-1112 — Direct opening of external apps
- **Phase:** 2 (Evolution) — **Priority:** Should
- **Description:** When the user accepts a recommendation from FR-1111, the system opens the external app if installed or directs to the app store if not.
- **Acceptance criteria:**
  - Checks presence of the external app before attempting to open (no visible error if not installed).
  - If not installed, redirects to App Store / Google Play with the correct landing.
  - The transition is fluid: the user is never stuck between the app and the browser.
  - The open/install event is logged anonymously (without identity association) for aggregate impact metrics.

##### FR-1113 — Open architecture for future integrations
- **Phase:** 1 (MVP, architectural preparation) — **Priority:** Must
- **Description:** The architecture allows incorporation of new integrations (wearables, external apps, health platforms, calendars, podcasts, moderation systems, etc.) without structural redesign.
- **Standards mapping:** HL7/FHIR not required in MVP, but the internal structure must allow mapping to these standards in later phases (see § 4.10 NFR-M09, E15 in § 11.2).

##### FR-1114 — Third-party APIs and strategic partnerships
- **Phase:** 2 (Evolution) — **Priority:** Should
- **Description:** The system supports consumption and exposure of third-party APIs for strategic partnerships between platforms (Itabey ↔ other health/wellbeing apps, healthtech, corporate platforms, etc.).
- **Acceptance criteria:**
  - API gateway layer with OAuth 2.0 minimum authentication.
  - Public documentation of the exposed API.
  - Compliance with privacy restrictions (FR-904, NFR-PR): no API exposes individual data without explicit per-user consent.
  - Immediate revocation mechanism of access to any third party.

### 3.12 Risk detection and referral (FR-12xx)

#### FR-1201 — Detection and referral protocols
- **Phase:** 1 (MVP) — **Priority:** 🛡️ **NON-NEGOTIABLE — Must**
- **Detected signals:** Severe emotional risk, concerning medical symptoms, crisis signals, self-harm, marked deterioration, high-vulnerability patterns.
- **Expected behaviour:** Automatic activation of hard-stop (FR-208) with predefined responses, professional referral, emergency resources.
- **Acceptance criteria:**
  - Signal catalogue clinically validated by PI2 before deployment.
  - 0 critical false negatives in controlled testing (severe signals not detected).
  - < 5% false positives (tolerable: better to err cautious).

### 3.13 Account management, access modes, and tiers (FR-13xx)

> Cross-cutting functionality and architectural commitment. Operationalises § 1.5: the user account is a single persistent object; commercial access mode and functional depth are **two orthogonal axes** (access mode × depth tier), both modulable without data loss.

#### FR-1301 — Single persistent user account
- **Phase:** 1 (MVP) — **Priority:** Must
- **Description:** Each user owns a **single** account linked to her identity and longitudinal data. The account survives any change of access mode (free → individual, individual → B2B, B2B → individual at end of organisational contract) and any tier change.
- **Acceptance criteria:**
  - No account duplication on mode or tier change.
  - 100% of longitudinal data preserved on mode or tier change.
  - The user is **always the data owner**. The paying organisation (P5) is not the owner and cannot inherit the account.

#### FR-1302 — Commercial access modes
- **Phase:** 1 (MVP — free + individual + basic B2B via company code) / 2 (Evolution — full B2B with enterprise SSO) — **Priority:** Must (MVP) / Should (Evolution)
- **Modes:**
  - **Free** — limited functionality.
  - **Paid individual** — paid directly by the user.
  - **Organisation-sponsored (B2B)** — paid by a company, insurer, mutual, healthcare system, or other entity. Linkage via **company code or invitation (MVP)** or **enterprise SSO (Phase 2)**.
- **Acceptance criteria:**
  - The active mode is visible to the user at any time.
  - Mode change does not require re-onboarding or new consent for existing data.

#### FR-1303 — Mode migration without data loss
- **Phase:** 1 (MVP — free ↔ individual + free ↔ basic B2B) / 2 (Evolution — including full B2B) — **Priority:** Must (MVP) / Should (Evolution)
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
- **Phase:** 1 (MVP, in force from the first B2B client) — **Priority:** 🛡️ **NON-NEGOTIABLE — Must**
- **Description:** When an organisation (P5) sponsors a user's access, the organisation **never accesses** that user's personal data or individual conversations.
- **Acceptance criteria:**
  - The organisation only accesses aggregated, anonymous metrics (overall usage, aggregate satisfaction, cohort trends). Never individual.
  - Any additional sharing (e.g. sending a report) requires explicit, revocable user action.
  - Technically auditable: a malicious organisation can never correlate usage with individual identity.
  - Minimum cohort size for aggregate reports: ≥ 10 active users (project proposal).

#### FR-1305 — Professional patient-management profile
- **Phase:** 2 (Evolution, not built in MVP) — **Priority:** Could
- **Description:** Reserve the possibility of a professional profile (clinician, social worker, health coach) able to manage several users/patients who have given explicit consent.
- **Architectural acceptance criteria (required of MVP vendor):**
  - The role and permission system (NFR-S04) allows incorporating this role without structural redesign.
  - The consent model (FR-904) lets the user authorise a specific professional's access to a granular subset of her data for a configurable period.
  - The data model anticipates an N-to-M relation between professional managers and users.
- **Distinction from PI2 (clinical team):** PI2 validates generic clinical knowledge for the entire system. The future professional manager (P7) manages individual patients with explicit consent.

#### FR-1306 — Functional depth tiers (architectural capability)
- **Phase:** 1 (MVP, architectural capability) / 2 (Evolution, operational tiers) — **Priority:** Must (MVP capability) / Should (Evolution operation)
- **Description:** The system supports **distinct functional depth tiers** that can be activated or deactivated by user, cohort, or contract without code changes. The PRD **does not prescribe** which features belong to which tier — that decision is deferred to product based on real usage signal. What is required is the **architectural capability** from day 1.
- **Per-tier parameterisable axes (non-exhaustive):**
  - Asha **long-term memory** depth (FR-204): time horizon, simultaneous patterns, pattern granularity.
  - **Insight frequency and depth** (FR-209): proactive vs on-demand only.
  - **Asha personalisation** (FR-601): number of available tones, language levels, focus modules (FR-603).
  - **Access to advanced panels** (FR-302 self-knowledge, FR-304 body): visibility and depth.
  - **Available integrations** (FR-104, FR-1101–1114): which wearables, calendars, and external apps connect.
  - **Report volume** (FR-401–403): number, frequency, format.
  - **Resource consumption quotas**: LLM calls, vector storage, tokens, voice processing.
- **Acceptance criteria:**
  - Any § 3 feature can be enabled/disabled per tier via configuration (not by code deployment).
  - Every tier has **defined and observable resource quotas**; no tier is "unlimited" without a cap.
  - Tier change is transparent to the user (data intact, configurations preserved) and reversible.
  - At least **3 parameterisable tiers** supported from the MVP (concrete names and contents to be defined later by product/commercial).

#### FR-1307 — Dynamic feature activation (feature flags as a capability)
- **Phase:** 1 (MVP) — **Priority:** Must
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
| NFR-S04 | Granular RBAC role-based access control — supports both MVP roles and later incorporation of additional roles (professional manager, etc.) without redesign |
| NFR-S05 | Activity logs and internal access audit |
| NFR-S06 | Full traceability of critical changes (knowledge versioning, consent changes, access by clinical role, feature flag changes, tier changes) |
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
| NFR-PR09 | 🛡️ **Data philanthropy model** (General Framework § 7.6): anonymised aggregate data may be used for scientific research / institutional collaboration with explicit consent; **never** sold as a commercial product |

### 4.5 Compatibility (NFR-C)

| ID | Requirement |
|----|-------------|
| NFR-C01 | iOS 16+ and Android 12+ in MVP |
| NFR-C02 | Responsive web (Chrome, Safari, Firefox, Edge versions N and N-1) |
| NFR-C03 | Screen-reader compatibility (VoiceOver, TalkBack, NVDA) |
| NFR-C04 | Apple Health (iOS) and Google Health Connect (Android) compatibility |
| NFR-C05 | Native deep-link support: iOS Universal Links + Android App Links (preparation for FR-1110 to FR-1112) |

### 4.6 Scalability (NFR-SC)

| ID | Requirement | Target |
|----|-------------|--------|
| NFR-SC01 | Year 1 registered users | 10,000–30,000 (aligned with pitch deck) |
| NFR-SC02 | Year 1 monthly active users | 3,000–10,000 |
| NFR-SC03 | Growth capacity without structural redesign | Up to 50,000 users |
| NFR-SC04 | Modular architecture with feature flags |  |
| NFR-SC05 | Progressive rollout and functional rollback |  |
| NFR-SC06 | **Functional modularity as first-class architectural capability** — every § 3 feature activatable/deactivatable via configuration (FR-1306, FR-1307). No rigid dependencies preventing tiering. |  |
| NFR-SC07 | **Per-tier resource quotas** (LLM, vector storage, tokens, voice) configurable and observable without code changes |  |

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
| NFR-I01 | **MVP supports Spanish as primary language** and English as secondary, with emphasis on Spanish-speaking cultural sensitivity (Spain, LATAM, Hispanic communities in the US) |
| NFR-I02 | Architecture ready to add additional languages without redesign (post-MVP: Brazilian Portuguese, others) |
| NFR-I03 | Educational content, interface, and conversational engine independently translatable |
| NFR-I04 | Cultural adaptation: tone, examples, cultural references adaptable by country/region. Each new geographic expansion requires cultural validation by local professional (General Framework § 9) |

### 4.9 Deployment and data sovereignty

| ID | Requirement |
|----|-------------|
| NFR-D01 | 🛡️ Deployment in European cloud (specific provider proposed by vendor) |
| NFR-D02 | Personal data processing within the EU |
| NFR-D03 | Subprocessor documentation with international transfer justification if any. **Attention:** expansion to LATAM and US (NFR-I01) requires specific analysis of international transfers |

### 4.10 Support, maintenance, and post-launch operations

| ID | Requirement |
|----|-------------|
| NFR-M01 | Evolutionary and corrective maintenance plan documented by vendor (E9) |
| NFR-M02 | Incident response times by severity (vendor-proposed; minimum target: critical < 4 h, high < 24 h, medium < 5 working days) |
| NFR-M03 | Technical support available at least during European business hours |
| NFR-M04 | Recurring monthly cost broken down: infrastructure, LLM models, voice, vector storage, human support (E14) |
| NFR-M05 | Cost estimation by scenario per 1,000 active users (low, medium, high) |
| NFR-M06 | Documented exit plan **anti vendor lock-in** (E16): how Polymita Systems would continue without the vendor in fewer than N weeks |
| NFR-M07 | Operational runbooks for frequent incidents delivered at project closure |
| NFR-M08 | Critical security updates with specific SLA (target: < 72 h post-detection) |
| NFR-M09 | **Documented HL7/FHIR readiness** (E15): data model mapping to these standards and evolution plan without structural redesign |
| NFR-M10 | Commitment to update tier (FR-1306) and feature flag (FR-1307) runbooks whenever the feature matrix changes |

---

## 5. User flows (primary flows)

### 5.1 F1 — Day 1 onboarding

**Personas:** P1, P2, P3.

1. User downloads the app and logs in / signs up.
2. **Privacy screen:** clear explanation of data treatment (GDPR Art. 9); granular consents (Asha memory, integrations, aggregate use, shared panel, external app recommendations).
3. **Focus** selection (scientific, integrative, emotional, wellbeing, spiritual, complementary — multi-select allowed; in MVP the selection is informational and translates into FR-603 in Phase 2).
4. Asha **tone** and **language level** selection.
5. Conversational mini-tutorial: Asha introduces herself, explains limits (FR-207), invites first entry.
6. Assisted first entry (manual or voice).
7. First contextual Asha response + mandatory disclaimer.
8. Suggestion to set up wearable and calendar integration (skippable).
9. (If B2B user) Company-code linkage screen (FR-1302).

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

1. User opens self-knowledge panel (FR-302).
2. Detected pattern: *"Your energy drops recurrently 2 days before your cycle."*
3. User taps the pattern → Asha contextualises with validated RAG.
4. Asha recommends educational capsule or logs an observation.
5. User optionally adds personal goal or shares the pattern.

**Success criterion:** ≥ 50% of monthly active users open the self-knowledge panel at least once a month (Evolution).

### 5.4 F4 — Generating a report for a healthcare professional (Phase 2)

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
4. System shows localised emergency resources by country (Spain: 024 suicide helpline + 112; LATAM and US: local equivalents).
5. Asha offers (with consent) to contact a preconfigured trusted person or healthcare professional.
6. System logs the event for clinical audit with metadata (no conversational content).

**Success criterion:** 100% of severe signals activate hard-stop. 0 incidents of free generative response to a severe signal.

### 5.6 F6 — B2B linkage from company code (MVP)

**Personas:** P5 (corporate client) + B2C user transitioning to B2B.

1. The organisation (P5) generates a company code in its dashboard (FR-1006).
2. The organisation shares the code with its employees (internal channel).
3. The employee (existing or new user) enters the code in Itabey's account section.
4. System validates the code and links the account to B2B mode (FR-1302).
5. The employee's account retains all previous data if any (FR-1303).
6. The organisation sees the employee as an anonymous aggregate number in its dashboard (FR-1006), never as an individual identity (FR-1304).

**Success criterion:** Linkage completed in < 2 minutes. 0 leaks of individual identity to the organisation.

### 5.7 F7 — External app recommendation (Phase 2)

**Personas:** P1, P2, P3.

1. During an Asha conversation or panel use, the user expresses a complementary need ("I can't sleep", "meditation helps me but I can't find time", etc.).
2. Asha detects the pattern and, if the user has opted in (FR-904), recommends a specific external app from the curated catalogue.
3. The recommendation includes: name, reason, disclaimer ("not clinical advice"), transparency indicator (affiliation or not), action buttons.
4. User taps "open/download":
   - If app installed: opens directly (FR-1112).
   - If not: redirects to App Store / Google Play.
5. System logs the event anonymously for aggregate metrics.
6. User can disable future recommendations of the same type at any time.

**Success criterion:** < 1% complaints about intrusive recommendations. ≥ 30% acceptance rate among opt-in users.

---

## 6. Constraints, assumptions, and dependencies

### 6.1 Technical constraints

| ID | Constraint |
|----|------------|
| TC1 | 🛡️ European cloud deployment |
| TC2 | 🛡️ Standard, maintainable tech stack — vendor proposes, justifies, avoids proprietary lock-in |
| TC3 | 🛡️ Asha decoupled from Itabey (API access) from day 1 |
| TC4 | Offline-first for data entry |
| TC5 | Multilingual Spanish + English from MVP, with Spanish-speaking cultural emphasis |
| TC6 | Native deep-link capability (iOS Universal Links + Android App Links) from MVP — preparation for FR-1110 to FR-1112 |

### 6.2 Business constraints

| ID | Constraint |
|----|------------|
| BC1 | Freemium model: limited free version + paid version + B2B sponsored |
| BC2 | No personal data sale |
| BC3 | Full intellectual property to Polymita Systems SL: code, architecture, prompts, embeddings, derived weights, RAG configurations, etc. |
| BC4 | Mandatory NDA and confidentiality with development vendor |
| BC5 | Multidisciplinary clinical team (PI2) validates all biomedical content |
| BC6 | Catalogue of recommendable external apps curated and validated before incorporation (no free LLM recommendations) |

### 6.3 Regulatory constraints

| ID | Constraint |
|----|------------|
| RC1 | 🛡️ Full GDPR compliance, including Art. 9 (health data) |
| RC2 | 🛡️ Asha is **not** a medical device. No diagnosis, no prescription, no professional substitution |
| RC3 | DPIA before launch |
| RC4 | Subprocessor and international transfer documentation (especially with LATAM / US expansion) |
| RC5 | Applicable regulatory compliance by jurisdiction (HIPAA in US in expansion phase, LGPD in Brazil where applicable, etc.) — Phase 2 |

### 6.4 Assumptions

| ID | Assumption | Risk if false |
|----|------------|---------------|
| A1 | Clinical team available before MVP to validate the initial knowledge base and hard-stop catalogue | Without validated content, the RAG engine cannot respond safely |
| A2 | GDPR compliance allows European cloud processing without additional transfers for Spain + EU | Any non-EU service dependency complicates compliance |
| A3 | Seed traction hypothesis assumes organic growth + modest paid acquisition + B2B channel | Metrics may need revision if acquisition strategy changes |
| A4 | Initial capsule catalogue (≥ 30) available or developed in parallel with the product | Without content, educational panel and RAG base are empty |
| A5 | Primary market is **Spanish-speaking** (Spain + LATAM + US Hispanics); each new expansion requires local cultural validation | If international strategy changes (rapid expansion outside Spanish-speaking markets), legal, language, and deployment implications apply |
| A6 | First B2B client in MVP is a controlled pilot with simple company code (no complex enterprise SSO) | If first client requires full enterprise SSO, MVP B2B scope overflows |
| A7 | Recommendable external app providers (FR-1111) willing to collaborate via deep links / agreements without requiring complex API integration in MVP | If they require complex API integration for the first use case, FR-1111 defers to advanced Phase 2 |

### 6.5 External dependencies

- Apple Health Kit, Google Health Connect (current SDK and terms).
- Google Calendar API, Apple Calendar API.
- European cloud provider (to be proposed by vendor).
- LLM and embeddings vendor (to propose; with no-training commitments on data).
- Voice vendor (TTS/STT) (to propose).
- Multidisciplinary clinical team (PI2) contracted/identified by Polymita Systems.
- App stores (App Store, Google Play) for deep links and app install redirection.
- External app providers (sleep, meditation, nutrition, etc.) — commercial agreements to be established in Phase 2.

---

## 7. Success metrics

> Target ranges are aligned with public benchmarks for longitudinal B2C healthtech and cycle apps (Flo, Clue, Natural Cycles) adjusted to Itabey's expected usage profile and Spanish-speaking audience. They will be refined with real data once the product is in market.

### 7.1 Activation

| Metric | Target | Measurement |
|--------|--------|-------------|
| % users completing onboarding | ≥ 70% | Funnel analytics events |
| % users with ≥ 7 days of entry in week 1 | ≥ 40% | Per-user entry events |
| Time to first useful Asha "insight" (self-reported or positive feedback) | < 72 h | First positive feedback timestamp |
| % B2B users completing company-code linkage | ≥ 85% | FR-1302 events |

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
| Free → individual paid conversion | 5–8% |
| Monthly paid churn | < 5% |
| LTV / CAC | ≥ 3 (post-launch at 6 months) |
| Active B2B clients by Month 18 | 2–3 (aligned with pitch deck) |

### 7.6 Scale

| Metric | Target |
|--------|--------|
| Year 1 registered users | 10,000–30,000 |
| Year 1 MAU | 3,000–10,000 |
| No-redesign capacity | 50,000 |

### 7.7 Community and content (Phase 2)

| Metric | Target |
|--------|--------|
| Forum DAU/MAU | ≥ 0.2 |
| Mean moderation time | < 24 h |
| Validated educational capsules / quarter | ≥ 15 |

### 7.8 External app integrations (Phase 2)

| Metric | Target |
|--------|--------|
| % users opted into external app recommendations | ≥ 30% |
| Acceptance rate of recommendations among opt-ins | ≥ 30% |
| % complaints about intrusive recommendations | < 1% |

---

## 8. Risks

| ID | Risk | Probability | Impact | Mitigation |
|----|------|-------------|--------|------------|
| R1 | Asha emits content interpretable as diagnosis (hallucination, jailbreak, edge case) | M | Critical | Strict RAG, hard-stop, visible disclaimers, clinical audit, red-teaming before launch |
| R2 | Sensitive data leak (GDPR Art. 9) | L | Critical | In-transit and at-rest encryption, layer segregation, pen-test, monitoring, least-privilege policy |
| R3 | Clinical team unavailable in time or insufficient | M | High | Early hiring, clear load definition, schedule slack |
| R4 | **Significant AI cost inflation over time** — LLM inference prices could multiply by 5–10× over the next 2–4 years, especially for frontier models; providers do not guarantee long-term price stability | H | Critical | (a) Multi-model architecture (FR-1306, NFR-SC07) allowing **LLM provider switching without redesign**; (b) **Mandatory hybrid mix:** open-source self-hosted models for structured tasks (classification, RAG, entity extraction) and large commercial models only where they add differential value; (c) Aggressive caching of similar responses; (d) Non-negotiable per-tier quotas from MVP; (e) Product pricing prepared to absorb inflation: tiers with clear quotas and B2B with consumption-based model beyond per-seat; (f) **Budget plan including inflation scenarios of 5×–10×** in inference cost, not just the central scenario; (g) Negotiation of reserved-capacity contracts with key LLM providers to mitigate price volatility |
| R5 | Excessive dependency on a single LLM vendor | M | Medium | Clear exit clauses, model abstraction layer, demonstrated portability in architecture |
| R6 | Community moderation crisis (Phase 2) | M | Medium | Proactive manual + AI moderation, clear policy, fast-block capability |
| R7 | Hard-stop false positives frustrate users | H | Low | Clinically validated catalogue, empathetic message on false positive, "this wasn't a crisis" feedback mechanism |
| R8 | Vendor technical lock-in on switch | M | High | Full IP clauses, contractual documentation, deliverable source code and architecture, NFR-M06 |
| R9 | User base rejects paid model | M | Medium | A/B test tiers, generous freemium, willingness-to-pay study |
| R10 | Insufficient GDPR compliance detected in audit | L | Critical | Early DPIA, EU healthtech specialist legal advice, external audit before launch |
| R11 | Vendor delivers monolithic architecture that hinders later tiering | M | High | Modularity and feature flags as evaluation criteria (FR-1306–1307, NFR-SC06–07, § 11.4); rejection of proposals lacking demonstration |
| R12 | B2B negotiates low volume prices while infrastructure/AI costs grow | M | High | Per-tier resource quotas from MVP (NFR-SC07), B2B pricing models based on consumption beyond per-seat, B2B tier with limited depth by default |
| R13 | B2C power users consume disproportionate resources in standard tier | M | Medium | Clear per-tier quotas (FR-1306), upgrade path to premium tier with cost aligned to delivered value |
| R14 | Tier strategy defined late, forcing product rebuild | L | High | Architectural capability from MVP (FR-1306–1307); commercial tier-content decision can be made at any time without redesign |
| R15 | LATAM expansion triggers international transfers complicating compliance | M | High | Specific legal analysis by country before each expansion, initial deployment focused on Spain, gradual expansion with updated DPIA |
| R16 | External app recommendations (FR-1111) perceived as intrusive advertising | M | Medium | Explicit opt-in in FR-904, clinically curated catalogue (no free LLM), "no more recommendations of this type" button, transparency about commercial affiliations |
| R17 | Insufficient cultural adaptation when expanding outside Spain (LATAM, US Hispanics) | M | Medium | Cultural validation by local professional before each expansion (General Framework § 9, NFR-I04) |

Probability: H/M/L. Impact: Critical/High/Medium/Low.

---

## 9. Verification strategy

> Mandatory PRD section: *"How will we know this is actually done — not just reported as done?"*

### 9.1 Functional verification

- **Automated tests** per FR — coverage ≥ 80% on critical flows (entry, hard-stop, report generation, B2B linkage).
- **Manual exploratory testing** per release with a script based on flows F1–F7.
- **Automated regression testing** in CI/CD.

### 9.2 Security and privacy verification

- **DAST/SAST** in every release.
- **External pen-test** before general launch and annually.
- **Documented GDPR audit** before launch.
- **DPIA** with specialised legal review in EU healthtech.

### 9.3 Clinical verification

- **Clinical team (PI2) reviews** every educational capsule before publication.
- **Hard-stop catalogue** reviewed and signed off by clinical team.
- **Clinical red-teaming** before launch: simulation of edge cases (self-harm, critical symptoms, emotional pressure) on Asha in staging.
- **Risk-detection testing** (FR-1201) on validated test corpus: 0 critical false negatives.
- **Validation of external app catalogue** (FR-1111) by clinical team before each incorporation.

### 9.4 Asha quality verification

- **Automated RAG eval suite**: retrieval precision, answer faithfulness (citation grounding), hallucination rate detected by judge.
- **Production feedback**: continuous FR-206 monitoring, alarm if % negative feedback exceeds threshold.
- **Weekly review** of anonymised samples of problematic responses.

### 9.5 UX and accessibility verification

- **WCAG 2.1 AA audit** before launch.
- **Real-user testing** representative of P1, P2, P3 (minimum 5 per persona, with Spanish-speaking cultural diversity).
- **Neurodivergent mode testing** with users in that profile.

### 9.6 Operational verification

- **Documented and rehearsed incident response plan**.
- **Runbooks** for Asha failures, integrations, hard-stop, external recommendations.
- **Observable metrics** (NFR-P, NFR-R) on 24/7 dashboards.

---

## 10. Glossary

| Term | Definition |
|------|------------|
| **Polymita Systems SL** | Owning entity of the project. Business and technological structure that supports the Itabey/Asha ecosystem. |
| **Itabey** | Platform and ecosystem name. Encompasses app, podcast, and future development lines. |
| **Asha** | Conversational engine and artificial intelligence of the ecosystem. Decoupled from Itabey via API, licensable to third parties as an independent product in Phase 2. |
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
| **Tier** | Configurable functional depth level of the product (see § 1.5, FR-1306). |
| **Feature flag** | Architectural mechanism that allows enabling/disabling functionality without redeploy (FR-1307). |
| **Deep link** | Link that opens a specific native application directly on a specific screen (iOS Universal Links, Android App Links). Technical basis for FR-1110 to FR-1112. |
| **Data philanthropy** | Model whereby anonymised data is used as a collective good for research and knowledge, without becoming a commercial product (General Framework § 7.6, NFR-PR09). |

---

## 11. Vendor evaluation criteria

> This section operationalises the requirements so received proposals can be compared structurally.

### 11.1 Required demonstrable capabilities

- Development of scalable mobile + web applications (verifiable references).
- HealthTech or sensitive-data treatment (GDPR Art. 9).
- GDPR compliance, Privacy/Security by design.
- Conversational AI with RAG architecture in production.
- Integration with external APIs (Apple Health, Google Health Connect minimum).
- Internal dashboard design with permission systems.
- Deployment and operations on European cloud.
- Evolutionary maintenance and deliverable technical documentation.
- Demonstrated modular architecture capability with feature flags and tiering.

### 11.2 Required deliverables in the proposal

| ID | Deliverable |
|----|------------|
| E1 | Technical proposal with recommended architecture |
| E2 | Specific AI architecture (RAG, models, voice, vector, cost control) |
| E3 | Contractual delivery milestones within Phase 1 (with associated payments, validable by Polymita Systems before continuing) |
| E4 | Time estimation per milestone |
| E5 | Cost estimation broken down (development, infrastructure, tokens/inference, voice) |
| E6 | Infrastructure cost estimation by scenario (1,000 active users: low, medium, high) |
| E7 | Assigned team with roles and experience |
| E8 | Proposed tech stack with justification and portability |
| E9 | Post-launch maintenance plan (evolutionary + corrective) with severity-based SLAs and support hours |
| E10 | Security measures and test plan |
| E11 | Identified technical risks with mitigations |
| E12 | Documented delivery plan to avoid structural vendor dependency |
| E13 | **Explanatory video** (FR-702) production / integration plan: vendor's internal production, externalisation to a content partner, or player only + integration (Polymita provides video) |
| E14 | **Recurring monthly cost** broken down by component (infrastructure, LLM, voice, vector, human support) and low/medium/high scenarios per 1,000 active users |
| E15 | **Architectural readiness document for HL7/FHIR**: how the data model can be mapped to those standards in a later phase without structural redesign |
| E16 | **Migration / exit plan** (anti vendor lock-in): how Polymita Systems would continue operating without the vendor, with time and cost estimate |
| E17 | **Demonstration of modular architecture and tiering capability** (FR-1306, FR-1307): prior project reference or technical proof showing feature flags as a first-class architectural capability, not as an add-on |
| E18 | **Integration plan for external apps and deep links** (FR-1110 to FR-1114): how architecture will be prepared from MVP and how functionality will be activated in Phase 2 |

### 11.3 Project-closure deliverables

- Full source code under Polymita Systems SL ownership.
- Comprehensive technical documentation (architecture, integrations, runbooks).
- NDA and commitment of non-reuse of project-specific components.
- Commitment not to generate derivative products based on Itabey/Asha logic.

### 11.4 Weighted evaluation criteria (proposal)

> Indicative weights. The organisation may adjust them based on its strategic priorities before initiating the evaluation.

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
> - A proposal must present **contractual milestones within Phase 1** (E3) with associated payments; proposals demanding single payment without intermediate milestones are rejected due to risk of losing control over cost and timeline.

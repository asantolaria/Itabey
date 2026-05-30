# Itabey / Asha — PRD (investor edition)

**Owning entity:** Polymita Systems SL
**Date:** 2026-05-30
**Version:** 4.0
**Audience:** seed-round investors

> This document is a condensed, non-technical version of the PRD intended for investors. It covers product vision, market opportunity, business model, execution plan and investment criteria. The full PRD (functional requirements, architecture, vendor evaluation criteria) is available in the developer-facing version.

---

## 1. Vision and value proposition

**Itabey** is a digital platform for longitudinal women's health support. **Asha** is the conversational AI engine integrated within Itabey. Together they form an ecosystem that records, interprets and accompanies women's bodily experience over time.

The core value proposition is not in data capture — increasingly commoditised by wearables and tracking apps — but in **contextualised longitudinal interpretation** backed by a clinically validated, versioned knowledge base maintained by a multidisciplinary medical team. Asha **does not diagnose, does not prescribe and does not replace medical consultation**. What it does is understand context, detect patterns missed by isolated consultations, generate non-clinical hypotheses, and provide companionship with judgement, sensitivity and rigour.

**18-month objectives:**

- Launch of the app + Asha operational, with 10,000–30,000 registered users in Year 1.
- Free → premium conversion of 5–8%.
- 2–3 active B2B pilot contracts by month 18.
- ARR of €120,000–240,000.
- Built clinical knowledge base that becomes a defensible, licensable asset.

---

## 2. Market and opportunity

### Priority market

US Hispanic-speaking community. Approximately **35 million Hispanic women** with:

- **High purchasing power** and stronger willingness to pay recurring subscriptions than in European or Latin American Spanish-speaking markets.
- **Strong digital health adoption**.
- **Specific cultural deficit**: leading platforms (Flo, Clue, Natural Cycles) are developed from an Anglo-Saxon cultural lens; even when translated, they do not reflect the Hispanic and Latina experience around the body, family, emotionality and self-care.

Spain, LATAM and other Spanish-speaking markets are **accessible from launch**, but the initial commercial focus concentrates on US Hispanic for effort-to-return reasons.

### Long-term sizing

Over 170 million Spanish-speaking women globally, with penetration projections at years 3–5:

| Penetration | Users | Estimated annual revenue |
|---|---|---|
| 0.02% (very conservative) | 34,000 | €2.9 M |
| 0.05% (conservative) | 85,000 | €7.1 M |
| 0.1% (base) | 170,000 | €14.3 M |
| 0.25% (moderate) | 425,000 | €35.7 M |
| 0.5% (optimistic) | 850,000 | €71.4 M |

*Subscription €10/month adjusted by 70% annual retention. Does not include B2B revenue or technology licensing.*

---

## 3. Product

### 3.1 Phased vision

The product is built in **two phases** for proposal evaluation and development planning purposes. Verticals and expansions are contemplated in a third long-term evolution phase.

| Phase | Horizon | Scope |
|---|---|---|
| **Phase 1 — MVP (commercial launch)** | Initial launch | Product core: Asha conversational engine, structured tracking, main panel, internal calendar, basic reports, careful onboarding, full privacy and security, initial health integrations, risk detection, basic B2B operational |
| **Phase 2 — Evolution** | 12–24 months post-launch | Community, advanced self-knowledge panel, interactive body map, shared panel, full B2B with enterprise SSO, bidirectional sync with external calendars, complementary external app recommendations, reports for healthcare professionals |
| **Phase 3 — Verticals** | 24+ months post-launch | Women's sports vertical, male adaptation, professional patient-management profile, API licensing and white-label of Asha, clinical interoperability (HL7/FHIR), scientific research with institutions, international expansion beyond Spanish-speaking markets |

> Detail of each phase and future vertical is developed in the complementary *Vision and roadmap* document.

### 3.2 MVP focus

The MVP concentrates the **five core pillars** validating the product's value proposition:

- **Asha** — conversational engine with RAG architecture, selective memory, text and voice conversation, non-diagnostic hypotheses, visible disclaimers, clinically validated hard-stop catalogue.
- **Tracking** — structured recording of cycle, symptoms, emotions, habits, sleep and events. Offline-first operation.
- **Insights** — basic longitudinal pattern detection. Initial self-knowledge panel.
- **Internal calendar** — canonical view of the user's cyclical information.
- **UX** — intuitive experience with cross-cutting modes (crisis mode, activatable neurodivergent mode), accessibility and multilingual.

**Functionality explicitly out of MVP** (with architecture prepared to add in Phase 2 without redesign): forum/community, shared panel, 3D body map.

### 3.3 MVP functionality by area

The following describes the concrete functionality the MVP will deliver, organised by area. This list summarises the functional scope of the technical PRD in non-technical language:

**Data capture and recording:**

- Manual recording of cycle, symptoms, emotions, habits, sleep and life events.
- Structured voice recording in natural language ("got my period today", "my lower back hurts", "slept badly").
- Automatic import of biometric data from Apple Health and Google Health Connect (sleep, activity, heart rate, temperature, HRV).
- Import of relevant events from Google Calendar and Apple Calendar (medical appointments, life events, travel).
- *Offline-first* operation: any recording persists without connection and syncs when restored.

**Conversation with Asha:**

- Text and voice conversation, with configurable voice, accent, speed and tone.
- Responses backed by a clinically validated knowledge base (RAG architecture): if confidence is low, Asha responds "I have no validated information on this" instead of inventing.
- Selective long-term memory (patterns, useful conclusions), not the complete conversation. The user can inspect, edit and delete what is remembered about her.
- Generation of non-diagnostic hypotheses, pattern detection, observation suggestions and recommendation of professional consultation when appropriate.
- **Visible and persistent disclaimers** ("Asha does not diagnose", "Asha does not replace a healthcare professional", "Asha may make mistakes").
- **Hard-stop protocol** for severe signals: when severe emotional risk, self-harm or medical emergency is detected, Asha suspends generative response and activates predefined clinically validated messages with redirection to emergency resources.
- Quick feedback per response (useful / not useful / problematic / simpler / deeper) feeding internal quality metrics.

**User panels and information:**

- Main panel with current state, contextual summary, cycle phase and quick access.
- Internal calendar with hormonal cycle, menstruation, estimated ovulation and fertility, lunar phase, manual events and soft predictions.
- Self-knowledge panel in initial version: basic detected patterns, longitudinal evolution, time-series charts.
- PDF report generation with longitudinal evolution of symptoms, cycle, mood, patterns and recommendations.

**Personalisation and onboarding:**

- Progressive conversational onboarding (without overwhelming the user with decisions from minute one).
- Asha tone selection (direct, empathetic, technical, realistic, soft, structured), language level (simple, technical, advanced) and voice/accent.
- Short explanatory video integrated in the product, accessible from onboarding and from a permanent help menu. Subtitles and offline playback if cached.
- Cross-cutting modes: crisis mode (for difficult days, simplified interface), activatable neurodivergent mode (stimulus reduction, low cognitive load).

**Notifications:**

- Soft notifications system, configurable by the user: recording reminders, cycle alerts, incomplete-record alerts. Non-invasive by default.

**Privacy and data control:**

- The user sees at any moment which data is stored about her.
- Full export of her data in structured format.
- Total deletion with explicit confirmation (right to be forgotten).
- Granular and revocable consent for each use of data (Asha memory, integrations, aggregated use for research).
- Pause tracking without data loss.

**Internal dashboards:**

- Administration dashboard (Founder / Super Admin) with global system metrics and management tools.
- Clinical dashboard restricted to the clinical team for validation of content and biomedical knowledge (without access to individual data or conversations).
- Corporate dashboard for B2B clients with anonymous aggregate metrics, population wellbeing metrics, ROI indicators and prevention tools.

**External integrations:**

- Apple Health (iOS) and Google Health Connect (Android) — initial health integrations.
- Event import from Google Calendar and Apple Calendar.
- Architecture prepared for future integrations with advanced wearables, complementary external apps (sleep, meditation, nutrition), HL7/FHIR and third-party APIs.

**Account and tier management:**

- Single persistent account per user, independent of access mode (free, paid individual, sponsored by organisation).
- Migration between modes without data loss (free ↔ individual ↔ sponsored).
- Corporate linkage via company code in MVP (full enterprise SSO in Phase 2).
- Non-negotiable B2B privacy: the organisation never accesses personal data or conversations.
- Modular tiering capability: the system can activate or deactivate features per user, cohort or contract without code changes (at least 3 parameterisable tiers from MVP).

### 3.4 Key product flows

Five flows described in the PRD to understand how the system is used in practice:

**Onboarding (Day 1):**

The user downloads the app, sees a clear privacy screen with granular consents, selects the focus that interests her most (scientific, integrative, emotional, wellbeing, spiritual, complementary), chooses Asha's tone and language level, receives a conversational mini-tutorial, makes her first assisted recording and receives Asha's first contextual response with disclaimer. **Success criterion**: ≥ 70% of users complete onboarding in one session.

**Daily recording (everyday use):**

The user opens the app or responds to a soft notification, records her day by voice or text ("got my period today", "slept very badly"), Asha extracts intent and entity, the user confirms or corrects, the data is recorded and reflected in panel and calendar. **Success criterion**: complete recording in under 30 seconds in 95% of cases.

**Longitudinal pattern consultation:**

The user opens the self-knowledge panel, sees a pattern detected by Asha ("your energy drops recurrently 2 days before your cycle"), Asha contextualises with the validated knowledge base, recommends a related educational capsule or records an observation. Optionally the user adds a personal goal or shares the pattern.

**Generating a report for a healthcare professional (Phase 2):**

The user asks Asha "prepare a report for my doctor", chooses time range and focus, Asha generates a structured clinical summary with symptoms, correlations, evolution and relevant entries, the user reviews and approves, the system generates a PDF with mandatory disclaimer.

**Crisis protocol (hard-stop, non-negotiable cross-cutting):**

The user expresses a severe signal (self-harm, intense emotional crisis, medical emergency), the system detects it automatically and suspends Asha's generative response, offers a clinically validated predefined message, shows local emergency resources (country-specific crisis lines) and optionally offers to contact a preconfigured trusted person. **Non-negotiable criterion**: 100% of severe signals activate hard-stop, 0 incidents of free generative response to severe signals.

### 3.5 Product commitments

Quality, security, privacy and operations guarantees the product must meet. For each commitment we state "what we guarantee", not "how we measure it" (that's in the technical PRD):

**Performance and experience:**

- Asha responds by text in under 5 seconds for standard queries (10 seconds for queries requiring deep search in the knowledge base).
- Asha responds by voice in under 3 seconds for short responses.
- The app opens and shows content in under 3 seconds on a 4G network.
- Any manual recording persists and is visually confirmed in under 2 seconds.

**Reliability and availability:**

- Monthly availability of 99.5% or higher once in production.
- Offline-first operation: 100% of core recording features available without connection.
- If Asha or an external integration fails, the application remains operational with a clear message and local recordings preserved.
- Daily encrypted backups in a separate European repository.

**Security:**

- Data encryption in transit (TLS 1.3) and at rest (AES-256).
- Robust authentication for users and mandatory two-factor authentication for internal roles.
- Granular role-based access control (RBAC) — the clinical team member does not see business metrics, the moderation member does not see clinical data, etc.
- Activity logs, internal access audit and traceability of critical changes.
- Regular security testing (DAST/SAST, pen-test before each major release).
- Deployment prepared for external security audits.

**Privacy (non-negotiable):**

- Full GDPR compliance with Art. 9 treatment for health data.
- Explicit, granular and revocable consent by the user for each use of her data.
- Minimisation: only what is necessary for the active feature is requested.
- Anonymisation and architectural separation between individual and aggregate data.
- Right to be forgotten implemented at pipeline level (not just logical deletion).
- **No sale of personal data under any circumstances.**
- DPIA (Data Protection Impact Assessment) carried out before launch.
- *Data philanthropy* model: aggregated anonymised data may contribute to research with explicit consent, **never as a commercial product**.

**Compatibility and accessibility:**

- iOS 16+ and Android 12+ in MVP.
- Responsive web (Chrome, Safari, Firefox, Edge).
- Compatibility with screen readers (VoiceOver, TalkBack, NVDA).
- WCAG 2.1 AA level minimum.
- Voice-only mode for non-sighted users.
- Activatable neurodivergent mode: stimulus reduction, simplified navigation, low cognitive load.
- Dark mode as a complete adaptation of the visual system.

**Scalability:**

- Support for 10,000–30,000 registered users in Year 1 without redesign.
- Capacity to grow to 50,000 users without structural redesign.
- Modular architecture with feature flags and per-tier configurable resource quotas.

**Internationalisation:**

- Support for Spanish (with Spanish-speaking cultural sensitivity) and English from MVP.
- Architecture ready to add additional languages without redesign.
- Each new geographic expansion will require cultural validation by local professional.

**Deployment and data sovereignty:**

- European cloud deployment (non-negotiable).
- Processing of personal data within the EU in first phases.
- Documentation of subprocessors with justification of international transfers (especially relevant with US expansion).
- Architectural readiness for HIPAA compliance given the priority market US.

**Post-launch support and maintenance:**

- Documented evolutionary and corrective maintenance plan.
- Incident response times by severity: critical < 4 hours, high < 24 hours, medium < 5 working days.
- Technical support available at least during European business hours.
- Recurring monthly cost broken down and documented migration / exit plan (anti vendor lock-in).

### 3.6 Differentiation: Asha as a defensible asset

Asha is designed from the outset as an **independent and decoupled engine** from the Itabey application, accessible via API. This enables it to be licensed to clinics, insurers, healthcare systems or digital health platforms as white-label technology in later phases.

Asha's defensibility comes from the **combination of four elements**:

1. **Biomedical knowledge base validated and versioned** by the clinical team (the corpus feeding the engine; no one else has it).
2. **RAG architecture** (Retrieval-Augmented Generation) where every response is backed by controlled sources, not by what an AI model "knows" on its own.
3. **Modular tiering capability** offering distinct depth levels per client (individual, corporate, licensed) without building parallel products.
4. **Network effects** derived from anonymised collective learning over time.

---

## 4. Users and segments

The system serves three primary B2C users, one corporate B2B persona, and architecturally provides for future profiles (professional managers, male adaptation).

### 4.1 Primary B2C personas

- **The curious self-learner (28–40)** — woman without diagnosed condition, seeks to understand her body and optimise wellbeing through self-knowledge.
- **The chronically symptomatic (30–50)** — lives with a cyclical condition (endometriosis, PCOS, perimenopause, cyclical mental health); needs to understand her condition and communicate better with her medical team.
- **The athlete (22–38)** — advanced or semi-professional practitioner; wants to adjust training and recovery to her hormonal cycle.

### 4.2 Corporate B2B client

Companies, insurers, mutuals and healthcare systems that fund access to Itabey/Asha for their employees or insured as a wellbeing and women's health benefit. **B2B is a strategic line from the outset** of the project, not a later add-on.

The corporate offering, from the MVP, includes not only licence management but:

- Anonymous aggregate usage analytics.
- Population wellbeing metrics.
- Impact tracking and ROI elements.
- Prevention tools.

**Non-negotiable privacy**: the organisation **never** accesses individual personal data or conversations. Only aggregates with minimum cohort size ≥ 10–20 active users.

### 4.3 Internal team and operation

The system contemplates five internal profiles that operate the product from Polymita Systems. Each with its dashboard, capabilities and clearly delimited restrictions:

- **Founder / Super Admin** (Mariela and management team): global system supervision, business metrics, feature flag and tier management, Asha quality supervision, content and knowledge editing, community moderation. Access to sensitive individual data only in specific contexts of support, security or moderation; always audited.
- **Multidisciplinary clinical and scientific team**: identified professionals in family medicine, gynaecology, mental health, endocrinology, anaesthesia and pain, molecular biology, biochemistry and neurosciences. Validate biomedical content, approve educational capsules, define general clinical criteria and sign off the hard-stop catalogue. **No access to individual user data or conversations.**
- **Community and forum moderation** (Phase 2 with forum activation): supervision and moderation of the community space, management of reported content, anti-spam tools, sensitive-content detection.
- **Analytics and data supervision** (Phase 2): aggregate analysis of system behaviour, cohorts, retention, data quality, Asha performance — always on anonymised data, never individual.
- **Senior technical supervision** (Phase 2): infrastructure, stability, security and overall technical performance monitoring. Read-only, no access to individual clinical data.

**Future profiles architecturally provisioned** (Phase 3): professional patient-management profile — clinicians, social workers or health coaches managing several patients who have given them explicit consent.

---

## 5. Business model

Three complementary revenue lines built progressively:

### 5.1 B2C — Individual subscription (MVP focus)

- **Freemium model**.
- **Free version** with limited functionality (product core).
- **Premium version at USD 17.99/month** with broad Asha use, long longitudinal memory, advanced configuration, detailed reports, sync with external calendars and other premium features.

### 5.2 B2B — Organisation-sponsored access (strategic line from MVP)

- Company-code linkage in MVP; enterprise SSO in Phase 2.
- Consumption-based pricing models beyond per-seat.
- Corporate dashboard with premium value proposition from the start.

### 5.3 Licensed technology (Phase 3)

- Asha as independent technology, licensable to clinics, insurers, healthcare systems or digital health platforms.
- Models: API licence, white-label, OEM.
- Higher margins than B2C because the architecture is already prepared.

### 5.4 18-month traction hypothesis

| Scenario | Registered users | % Premium | Active premium users | Active B2B contracts |
|---|---|---|---|---|
| Conservative | 10,000 | 5% | 500 | 1 |
| Base | 50,000 | 6% | 3,000 | 2–3 |
| Optimistic | 100,000 | 8% | 8,000 | 3+ |

Key metrics at 18 months (base scenario):

- D90 retention: 15–25%.
- Free → premium conversion: 5–8%.
- Monthly paid churn: 4–8%.
- LTV/CAC: ≥ 3 (post-launch at 6 months).
- Projected ARR month 18: €120,000–240,000.

---

## 6. Competitive differentiation

Four factors differentiating Itabey from existing solutions and building its defensible advantage:

### 6.1 Cross-cutting vision, not specialised

Itabey does not compete as "another cycle app" or "another wellbeing app". It integrates cycle, sleep, habits, emotions, biometrics and life context in a single experience. Asha understands how these variables interact — something no current platform does.

### 6.2 Defensible and licensable technology

The clinically validated knowledge base, RAG architecture and modular tiering capability are **proprietary assets of Polymita Systems**. Licensing Asha as an independent product is a future revenue line already prepared architecturally.

### 6.3 Modular architecture and financial resilience

The system is designed with a hybrid mix of AI models: open-source self-hosted models (≈70% of traffic, fixed cost) + commercial cloud models (≈30%, only where they add differential value). This delivers:

- **Lower cost per user** (3–5× lower than monolithic cloud-only).
- **Financial resilience** against the structural rise expected in AI costs in coming years.
- **Provider independence** (LLM provider switching without redesign).

### 6.4 Ethical data model and *data philanthropy*

Itabey **does not sell personal data** under any circumstances. Aggregated anonymised data can, with explicit consent, contribute to scientific research and academic institutions — always as collective good, not as commercial product. This is a differentiating ethical positioning that builds user trust and opens future institutional collaborations.

---

## 7. Architecture as competitive advantage (no jargon)

The architectural decisions relevant to the investor are three:

### 7.1 Asha decoupled from day 1

Itabey (the app) and Asha (the AI engine) communicate exclusively via documented API. This enables Asha to be **an independent product licensable to third parties** whenever commercially appropriate, without redesigning anything.

### 7.2 Hybrid AI mix

The combination of proprietary models (hosted on European infrastructure) + selective commercial cloud models gives cost control, AI price inflation resilience and provider independence. This decision **is financial, not technical**: over the next 2–4 years, sectoral sources (Moody's, Goldman Sachs, Gartner) forecast that net AI operating cost will rise structurally. A monolithic architecture amplifies any rise 3–5×. A modular hybrid one mitigates it.

### 7.3 GDPR compliance and HIPAA readiness

European cloud deployment in initial phases, full GDPR compliance with Art. 9 (health data), in-transit and at-rest encryption, DPIA before launch, **HIPAA readiness** given the priority market is US Hispanic.

---

## 8. Financial plan and use of funds

**Seed round requested: €1,500,000.**

### 8.1 Use of funds breakdown

| Category | Amount | % |
|---|---|---|
| Marketing and user acquisition | €350,000 | 23.3% |
| MVP development (App + Asha) | €350,000 | 23.3% |
| In-house core team | €280,000 | 18.7% |
| Operations and premises | €25,000 | 1.7% |
| Cloud infrastructure / AI | €90,000 | 6.0% |
| Specialist collaborators and validation | €50,000 | 3.3% |
| Legal and advisory | €35,000 | 2.3% |
| Hardware + production setup | €20,000 | 1.3% |
| Buffer and contingency | €300,000 | 20.0% |
| **Total** | **€1,500,000** | **100%** |

### 8.2 Consideration on AI cost evolution

The technical consultant's sectoral analysis indicates that **the net cost of operating AI will rise structurally** in a 2–4 year horizon, due to the combination of four forces (energy/infrastructure bottleneck, post-subsidy normalisation by LLM providers, growing consumption per application, frontier model costs). Sources consulted include Moody's, Goldman Sachs, Gartner, Epoch AI and specialist analysts.

For Itabey's base scenario (3,000 active premium users), expected annual overcost vs current cost:

| Scenario | Rise over current AI cost | Estimated annual overcost |
|---|---|---|
| Controlled rise (modular architecture well executed) | +50% to +100% | +€75,000 to +€150,000 |
| Intense rise (hard normalisation + aggressive consumption) | +200% to +400% | +€300,000 to +€600,000 |
| Uncontrolled rise (monolithic architecture) | +400% to +700%+ | +€600,000+ |

The factor most amplifying or mitigating the risk **is not market prices** (those are common to all actors), but **the architectural decision**. Itabey's modular architecture contains the rise in the controlled scenario.

**Polymita Systems plans to incorporate a specific financial buffer for AI** within the seed equivalent to **12–24 months of the AI cost of the base scenario** (approximately €150,000–300,000), in addition to the general contingency buffer.

If the conversation with the investor warrants it, **there is the option of expanding the round by €200,000–400,000 additional** specifically for reinforced AI buffer, keeping everything else. The decision is to be assessed with the investor based on risk appetite.

---

## 9. Verifiable milestones at 18 months

| Month | Milestone |
|---|---|
| 7 | MVP Launch — App + Asha operating after 5 months development + 2 months beta testing. 200–500 first active users. |
| 10 | First Traction Metrics — 1,000–2,000 registered users, positive qualitative feedback, first exploratory B2B contacts. |
| 15 | Consolidation of Organic Traction Metrics — 5,000–10,000 active users, first recurring revenue, product in continuous improvement. |
| 18 | Model Consolidation and Scaling — 10,000–20,000 users, ARR €120,000–240,000, 2–3 active B2B pilots, model validated for scaling. |

> **Note on time horizons**: the 18-month milestones are pitch-deck commitments. The horizons for Phase 2 (12–24 months post-launch) and Phase 3 (24+ months) are indicative estimates based on the scope of each phase and the CEO's response on the women's sports vertical. The specific implementation timelines will be adjusted by the development vendor in their technical offer.

---

## 10. Key risks and mitigations

| Risk | Probability | Impact | Mitigation |
|---|---|---|---|
| Asha emits content interpretable as clinical diagnosis (hallucination, edge case) | Medium | Critical | Strict RAG architecture, clinically validated hard-stop, visible disclaimers, pre-launch red-teaming, continuous clinical audit |
| Sensitive data leak (GDPR Art. 9 breach) | Low | Critical | Privacy by design, full encryption, pen-testing, monitoring, least-privilege policy, DPIA before launch |
| Structural rise in AI cost (5–10× in 2–4 years in adverse scenario) | High | Critical | Modular multi-model architecture, mandatory hybrid mix, per-tier quotas, specific financial buffer in seed, absorbent pricing |
| Clinical team not available on time or insufficient | Medium | High | Early identification and contracting (team already identified), responsibility on Polymita Systems with vendor coordination |
| Technical vendor lock-in upon developer change | Medium | High | Contractual full intellectual property clauses, documented migration plan, deliverable source code, no-lock-in architecture |
| Priority market US Hispanic activates HIPAA compliance from launch | High | Critical | Specific US legal analysis before launch (not after), specific DPIA for processing data of persons in US, documented strategy for HIPAA compliance |

---

## 11. Key constraints and assumptions

The structuring decisions of the project, articulated as technical, business and regulatory constraints, and the assumptions on which the plan is built:

### 11.1 Technical constraints

- European cloud deployment (non-negotiable in first phases).
- Standard, maintainable tech stack; the development vendor proposes and justifies, avoiding proprietary lock-in.
- Asha decoupled from Itabey via API from day 1.
- Offline-first operation for data recording.
- Multilingual Spanish + English from MVP, with Spanish-speaking cultural emphasis.

### 11.2 Business constraints

- Freemium model: limited free version + paid version + sponsored B2B.
- No sale of personal data under any circumstances.
- Full intellectual property to Polymita Systems SL: code, architecture, prompts, embeddings, configurations, derivative models.
- Mandatory NDA and confidentiality with the development company.
- Multidisciplinary clinical team validates all biomedical content before its publication.
- Curated and clinically validated catalogue of recommendable external apps.

### 11.3 Regulatory constraints

- Full GDPR compliance, with Art. 9 (health data).
- Asha is **not** a medical device: no diagnosis, no prescription, no professional substitution.
- DPIA before launch.
- **HIPAA readiness** from the outset given the priority market US Hispanic.

### 11.4 Key assumptions

- The clinical team will be available before the MVP to validate the initial knowledge base and hard-stop catalogue.
- GDPR compliance allows processing data in European cloud without additional transfers for the first phase.
- The initial catalogue of educational capsules (≥ 30) will be available or will be developed in parallel with the product.
- The first B2B client in MVP will be a controlled pilot with simple company code (not complex enterprise SSO yet).
- The traction hypothesis assumes organic growth + modest paid acquisition + B2B channel.

---

## 12. Investment terms

| Concept | Detail |
|---|---|
| **Investment** | €1,500,000 |
| **Equity stake** | Up to 30% |
| **Implicit post-money valuation** | ~€5 M |
| **Structure** | Single alliance, no further rounds envisaged |
| **Founder retention** | ≥ 70% of capital and operational control |
| **Governance** | One board seat for the investor; vote on relevant strategic decisions; operational management reserved to the founding team |
| **Investor rights** | Quarterly financial report, access to key business metrics (MRR, CAC, churn), semi-annual strategic update |
| **Legal clauses** | Standard shareholders' agreement, tag-along, drag-along |
| **Return horizon** | 5–7 years, with consolidated dividends or, if appropriate, a sale operation |

**Non-dilutive complementary funding envisaged:** ENISA, CDTI, European Next Generation funds, autonomous regional grants.

---

## 13. Team and advisory board

**Mariela Herrera Gil — Founder and CEO.** Project vision born from personal experience and years of self-directed research on hormonal regulation, neurodivergence, nervous system, inflammation, sleep and human behaviour. Responsible for strategy, brand identity and product direction.

**Identified multidisciplinary clinical and scientific team.** Profiles in family medicine, mental health, endocrinology, anaesthesia and pain, molecular biology, biochemistry and neurosciences. Some collaborate actively in the conceptual definition of the system; others will formally join as the funding phase progresses.

**Senior External Technical Consultant.** Independent technical support for proposal validation, architecture supervision and review of technical decisions during construction and product development.

**External development company.** To be selected through a structured proposal evaluation process with technical, financial, security and architectural modularity criteria defined in the technical PRD.

---

## 14. Why this project, why now

- **Real and underserved market**: the US Hispanic woman is a large segment, with purchasing power, high digital adoption and poorly represented by leading platforms.
- **Mature technology**: the combination of AI models, RAG and multi-model architectures now enables a product that 5 years ago was not viable at reasonable cost.
- **Defensible model**: the clinically validated knowledge base, decoupled licensable engine and modular tiering architecture build sustainable competitive advantage — not just a product.
- **Long-term vision**: the project is not just an app. It is a technology infrastructure that can evolve into an ecosystem of women's health with multiple revenue lines and applications to scientific research.
- **Ethical foundation**: no data sale, non-negotiable privacy, continuous clinical validation. A positioning that builds user trust and opens future institutional collaborations.

---

## Complementary documents

- **Full technical PRD** (Spanish and English) — for evaluation of development vendor proposals.
- **Vision and roadmap** — features, modules and future verticals (sports, male, professional manager, licensing, HL7/FHIR, research).
- **Consultant's analysis on AI cost evolution** — with cited sectoral sources.
- **Preliminary architecture proposal** — technical vision to support vendor evaluation.

---

*Confidential document. All rights reserved to Polymita Systems SL.*

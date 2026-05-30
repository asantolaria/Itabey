# Itabey / Asha — System Architecture: Executive Summary

**Date:** 2026-05-30
**From:** Alex Santolaria — Technical Consultant
**For:** Mariela Herrera Gil — Polymita Systems SL
**Purpose:** To give a clear understanding of how Itabey/Asha will be built technically, **without jargon**, sufficient to explain it to investors and understand why certain technical decisions are also business decisions.

> A detailed version of this document (`arquitectura-preliminar.md`) exists with technical depth for the team and vendors. This executive summary is the equivalent in accessible language.

---

## 1. Why architecture matters for Itabey

Architecture is the way the pieces of the product are organised internally. It is not a secondary technical detail: **it determines the cost of operating the product, how it scales, what can be licensed, the resilience against provider changes and how flexible you will be to adapt commercial tiers in the future**.

Three ideas to keep in mind for investor conversations:

- **Asha is not the app.** Asha is an independent AI engine the app uses, and which in the future can be licensed to third parties without touching anything else.
- **It is not "one AI" but several.** An architecture combining proprietary AI (cheap, private) with cloud AI (more capable, more expensive) lowers the cost per user by 3–5 times compared to an architecture using only cloud.
- **Modular means flexible.** The ability to activate and deactivate features per tier without touching code is what allows the product to be simultaneously free for some, premium for others and B2B corporate for companies, without building parallel products.

---

## 2. The four pieces of the system

The system is split into four pieces with clear and separate responsibilities. Each piece communicates with the others through well-defined channels.

### The application (the app the user uses)

What the user sees and touches: the mobile app on her iPhone or Android, and the web version. The calendar, panels, recording forms, conversation with Asha and all the screens live here.

The app does not make intelligent decisions or store definitive data: it only presents information, captures inputs and asks the platform for what it needs.

### The Itabey platform (the operational brain)

The heart of the system, what the user does not see directly but is always running behind. Here live:

- Accounts, passwords and permissions.
- Each user's data (cycle, symptoms, sleep, life events).
- The tier system (free, premium, B2B) and the mechanisms to activate and deactivate features.
- Notifications, generated reports, integrations with calendars and wearables.
- Internal team dashboards (admin, clinical team, etc.).

### The Asha engine (the conversational intelligence)

**The defensible asset lives here.** Asha is an independent service that communicates with the Itabey platform but could work on its own, connected to other platforms. This is done this way because:

- In the future we want to be able to **license Asha** to clinics, insurers or health platforms, without touching the Itabey app.
- If Asha grows or consumption increases, we can **scale it separately** without affecting the rest of the system.
- If in the future we want to change AI provider, we can do it **without redesigning the platform**.

### External integrations (bridges to other tools)

The piece that talks to external systems: Apple Health, Google Health Connect, Google Calendar, Apple Calendar and, later, advanced wearables and complementary external apps.

---

## 3. How Asha works inside (the conceptual logic)

The Asha engine has several sub-pieces. It is worth understanding the conceptual logic because it explains the costs and the asset's defensibility.

### The orchestrator (Asha's brain)

Every time the user interacts with Asha, an internal component —the orchestrator— makes a very important decision: **what type of AI to use for this specific task**. It is not the same to decide whether a sentence is "symptom recording" or "health query" (something simple) as to generate an empathetic, deep response about the user's sleep (something complex).

A good orchestrator is what enables Asha to work well at reasonable cost. A bad orchestrator (one always using the most expensive AI) can multiply cost by 5.

### Hybrid mix: two types of AI combined

Asha uses two types of AI in parallel:

- **Proprietary AI** (hosted on our own European infrastructure). It is cheap, private and fast. Used for structured tasks: classifying what the user says, extracting data like "headache" or "poor sleep quality", searching the knowledge base. **Approximately 70% of traffic goes through here.**
- **Cloud AI** (Anthropic Claude, or equivalent). More capable, more expensive, accessed via external service. Used for deep conversations, empathetic responses, medical report generation. **Approximately 30% of traffic goes through here.**

The 70/30 ratio is what makes the product's cost viable. If we did everything through expensive cloud AI, cost per user would multiply by 3–5.

### The clinical knowledge base (the defensible asset)

Asha does not respond from "what it knows" on its own. Before responding to anything about health, **it consults a clinical knowledge base validated and versioned by Itabey's medical team**. That base contains:

- Educational capsules approved by the clinical team.
- Safety and referral protocols (what to do in the face of risk signals).
- Validated general biomedical criteria.

**This knowledge base is the product's most defensible asset.** Nobody else has it; it has been built specifically for Itabey with your clinical team; it is versioned and updatable. It is what enables Asha to respond with rigour, not with invention, and what differentiates her from any generic chatbot.

### Memory per user (selective, not complete)

Asha remembers patterns, preferences and useful conclusions for each user, not the entire conversation. This is important for two reasons: for privacy (we do not store things we do not need) and for cost (more memory = more cost per message). The user can inspect, edit and delete what Asha remembers about her.

### Voice

Asha understands what the user says by voice (via a component called Whisper, hosted on our infrastructure) and responds in natural voice (via a high-quality cloud service). Voice quality matters because it is part of the differentiating experience: the user can record her day walking, driving or cooking.

---

## 4. Five key architectural decisions and what they mean for Itabey

| Technical decision                                  | What it means for the business                                                                                                                                                                  |
| --------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Asha is an independent service from day 1**       | You can license Asha to third parties in Phase 3 without redesigning anything. It is the technical foundation of the future licensing revenue line.                                             |
| **Hybrid mix (proprietary AI + cloud AI)**          | Cost per user 3–5 times lower than a "cloud-only" competitor + resilience against the structural rise of AI cost expected in coming years. **It is a financial decision, not a technical one.** |
| **Ability to switch AI providers without redesign** | If Anthropic, OpenAI or Google raise prices or shut down services, we can switch effortlessly. We negotiate better because no one has us trapped.                                               |
| **Modularity and tiers from day 1**                 | The same system serves free, premium individual and B2B corporate. We do not build parallel products. We can define tier contents with real data without technical works.                       |
| **European cloud + HIPAA readiness**                | Full GDPR compliance + readiness so that the priority market (US Hispanic) is regulatorily viable.                                                                                              |

---

## 5. The uncomfortable conversation: AI cost evolution

Four facts that sectoral sources tell us (Moody's, Goldman Sachs, Gartner, Epoch AI):

1. **The price of operating an AI conversation is falling** (per-unit prices have fallen 10× in 2 years; Gartner predicts -90% by 2030).
2. **But the monthly bill rises** because applications consume more per user (more memory, more interactions, more capabilities) as they mature.
3. **Current prices are subsidised** by venture capital: OpenAI loses $1.35 for every $1 it earns. When that policy ends (12–24 months), there will be a rise.
4. **There is a physical bottleneck**: electricity and chips for AI data centres are saturated, and that raises costs for both commercial cloud and those with proprietary infrastructure.

**Clear conclusion**: the net cost of operating AI is going to rise in net terms. The question is not whether it will rise but by how much. And the answer depends almost entirely on architecture:

| Scenario at 2–4 years                                                     | AI cost rise vs current |
| ------------------------------------------------------------------------- | ----------------------- |
| **Controlled rise** (modular architecture well executed)                  | +50% to +100%           |
| **Intense rise** (hard normalisation + aggressive use of advanced models) | +200% to +400%          |
| **Uncontrolled rise** (monolithic cloud-only architecture)                | +400% to +700%+         |

**It is not the market that decides which of the three scenarios Itabey lands in: it is the architectural decision.** This is why this proposal insists so much on the hybrid mix and on the ability to switch providers.

**Concrete financial implication**: it is advisable to reserve within the seed round a buffer equivalent to 12–24 months of the AI cost forecast for the base scenario (estimated at ~€150,000–300,000), in addition to the general buffer. Three options I detailed in a separate email (A: keep round, B: expand by €200–400K specifically for AI buffer, C: absorbent pricing from day 1). The decision is yours.

---

## 6. What this document does NOT decide

Worth being clear about when speaking with investors and vendors:

- **It does not fix the concrete technology stack** (which programming language, which exact tools, which cloud provider). The development vendor decides in its proposal.
- **It does not fix which specific AI model is used** (Claude vs GPT vs Gemini vs specific open-source). The vendor decides.
- **It does not fix specific versions of tools.**
- **It is not the final architecture** — it is a consultant's proposal to serve as **reference and benchmark** when comparing vendor proposals.

**What to do with proposals that arrive:**

- If a proposal generally fits this scheme, it is a good sign.
- If a proposal diverges significantly (all cloud without proprietary AI, monolithic system without Asha decoupled, no switch capability between providers), it is advisable to ask why before discarding — it may have valid reasons or be a sign of inexperience.
- The criteria in PRD § 11 are what determines final evaluation.

---

## In summary — for an investor conversation in one sentence

> *"Itabey and Asha are designed from day 1 with four decisions that protect the business: Asha decoupled for future licensing, hybrid AI mix to keep cost controlled, ability to switch providers without redesign to depend on no one, and modular architecture with tiers so that the same product serves very different clients. These decisions are not technical: they are financial and strategic."*

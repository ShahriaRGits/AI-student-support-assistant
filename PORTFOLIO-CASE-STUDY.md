# Northstar / study
## AI Student Support & Programme Recommendation Assistant

> **Case-study status:** Validated MVP prototype. The evidence below describes the implemented prototype, not a production deployment. Simulated catalogue data, in-memory lead storage, mocked-AI test behavior, and proposed production integrations are explicitly identified.

Northstar / study is a student-programme discovery experience designed to move a prospective student from an uncertain starting point to a grounded shortlist and a consented enquiry. The prototype combines a premium editorial interface, a structured assessment, server-side AI interpretation, deterministic programme matching, AI-generated explanations, comparison, lead capture, and an authenticated dashboard.

The implementation was validated with a TypeScript check, a production build, eight passing unit/integration tests, and visual review of the responsive landing-page experience. The case study deliberately reports no conversion, accuracy, engagement, or business metrics because none were measured.

## 01 Problem

Prospective students often begin programme discovery with a broad question rather than a precise search query: *What should I study next, and why would it fit me?* A catalogue-first experience makes the student translate their own background, interests, goals, budget, and location into filters before they have enough structure to make good choices.

The product problem for this MVP was therefore not simply “show programmes.” It was to create a guided path that captures the student’s context, turns it into a usable profile, narrows a fictional catalogue consistently, and explains the shortlist without pretending that AI knows facts the catalogue does not contain.

The prototype’s problem framing is evidenced by the landing-page copy, the four assessment dimensions, and the result-page language in the public workflow. It is a product hypothesis rather than a claim that the problem has been quantitatively validated.

## 02 User

The primary user is a prospective student who is exploring further study and wants a clearer starting point. The implemented assessment asks for academic background, interests, goals, budget, and location preference. This defines the prototype’s user model more precisely than an abstract “student” persona.

A secondary user is an admissions or programme team member who needs to review submitted interest and understand which fictional programmes are receiving attention. The dashboard is protected behind authenticated administrator access and surfaces enquiries, assessment summaries, and programme-interest summaries.

No user research study, interview sample, demographic segmentation, or validated persona metrics are included in the project evidence. Those would be appropriate follow-up research rather than facts to retrofit into this case study.

## 03 Context

The product was intentionally scoped as a low-cost, easy-to-demonstrate MVP. The implementation uses a modular full-stack web application with React and Tailwind on the client, Express/tRPC procedures on the server, Zod validation, the built-in server-side LLM helper, and the existing Manus authentication scaffold.[1] [2]

The context shaped several boundaries. The catalogue contains five fictional programmes, leads live in the server process for the demonstration, and the AI is instructed to work only from submitted assessment data and supplied programme fields. The demo guide explicitly states that the entries are not institution listings and must be verified before production use.[1]

This is a prototype context, not a live admissions or counselling context. It does not make eligibility decisions, submit applications, send information to institutions, or claim authoritative programme availability.

## 04 Product Opportunity

The opportunity was to make programme discovery feel more like thoughtful guidance than catalogue filtering. A student could receive value from a coherent interpretation of their own inputs even before any live institutional data existed.

The implemented opportunity has three parts. First, the questionnaire reduces the blank-page problem by asking focused questions. Second, deterministic matching makes the shortlist reproducible and inspectable. Third, AI adds a human-readable explanation while being constrained by the available data.

The product also creates a demonstrable handoff point: once a student has a shortlist, they can compare up to three programmes and submit an explicit-consent enquiry. In the prototype, that enquiry remains a simulated lead rather than a real institutional referral.[1]

## 05 User Journey

The implemented journey is a single public flow with five meaningful moments:

| Stage | Student action | Implemented response |
|---|---|---|
| Discovery | Opens the landing page | Sees the Northstar / study value proposition and a clear assessment CTA |
| Context | Completes four assessment steps | Enters background, interests, goals, budget, and location |
| Interpretation | Selects “See my matches” | Sees a dedicated processing state while the server interprets the assessment |
| Shortlist | Reviews programme cards | Sees scored matches, AI-generated reasoning, demo labels, and comparison controls |
| Action | Compares or enquires | Compares up to three programmes or submits name, email, phone, and explicit consent |

The suggested demonstration path then continues to `/dashboard`, where an authenticated administrator can review the captured enquiry and programme-interest summary.[1]

The transition states are part of the journey rather than afterthoughts. The client models `landing`, `assessment`, `loading`, and `results` states; the assessment also exposes an inline processing skeleton, while the results transition has a dedicated loading treatment.[2]

## 06 Product Requirements

The approved MVP requirements were translated into the following implemented capabilities:

| Requirement | Prototype implementation | Evidence boundary |
|---|---|---|
| Landing page | Branded hero, feature highlights, CTA, navigation | Verified in `Home.tsx` and landing screenshot |
| Assessment | Four-step structured questionnaire with validation gates | Implemented in `Home.tsx` and `assessmentSchema` |
| AI interpretation | Structured profile response with server-side LLM call and fallback | Implemented in `routers.ts`; fallback tested |
| Programme catalogue | Five fictional records with metadata | Simulated; not institution data |
| Matching | Deterministic score from tags, location, budget, and goal keywords | Implemented in `scoreProgram` |
| Recommendation reasoning | AI-generated paragraph with grounded fallback | Implemented and labeled in the UI |
| Comparison | Side-by-side view for up to three programmes | Implemented in results view |
| Lead capture | Name, email, phone, consent, assessment, selected matches | Zod-validated and tested |
| Dashboard | Admin-gated enquiries and programme-interest summary | Implemented with session-only lead storage |
| States | Loading, error, empty, and retry states | Implemented across public and admin surfaces |

The requirements describe the prototype’s scope. They do not establish production compliance, institutional accuracy, or measurable recommendation quality.

## 07 MVP Decisions

The most important MVP decision was to use a modular monolith rather than split the product into separate services. The assessment, matching engine, AI orchestration, lead capture, and dashboard can be understood and demonstrated as one application, which reduces deployment and debugging overhead.

A second decision was to keep deterministic logic outside the model. The programme catalogue is a server-owned array, and `scoreProgram` explicitly scores tag overlap, location compatibility, budget fit, and selected goal keywords. The model is used for structured interpretation and explanation, not as the sole source of truth for programme facts.[2]

A third decision was to use demo data instead of adding an external catalogue API. The project documentation states that the five programmes are fictional and must be replaced or verified before production. This kept the MVP reliable and inexpensive while making the boundary visible to the user.

A fourth decision was to keep lead storage in memory for the demonstration. That makes the flow easy to run but means the data is not durable. The demo guide identifies database-backed storage as a production follow-up rather than disguising the limitation.[1]

## 08 UX Design

The visual direction is an editorial student-guidance concierge. The landing screenshot shows an ivory background, deep green product card, large serif headline, muted body copy, green italic emphasis, orbit/path lines, and a restrained navigation system. The “DEMO EXPERIENCE” pill establishes the prototype context immediately.[3]

The visual system uses Playfair Display for expressive hierarchy and DM Mono for compact metadata and labels. The CSS defines deep-green, ivory, muted sage, lavender, and warm accent surfaces; rounded cards; restrained shadows; and short skeleton animations. The orbit, path, compass, and “direction” language carry the Northstar metaphor into the interface rather than presenting a generic dashboard aesthetic.[4]

The assessment uses a focused single-card layout with a progress indicator and one decision per step. Results use a profile banner, scored cards, fact groups, tags, reasoning blocks, and a comparison table. The lead form is a modal with an explicit checkbox and a visible statement that it is a demo enquiry.

Responsive behavior is implemented at an 800px breakpoint. Grids collapse to one column, CTAs stack, comparison columns become vertical, and the dashboard content becomes mobile-friendly.[4] The project records visual verification for desktop and mobile landing-page layouts.[1]

![Verified landing-page screenshot](../screenshots/webdev-preview-root-1786821451862943934-1601.png)

*Figure 1. Verified landing-page capture. The screenshot shows the branded hero, assessment CTA, demo label, programme-direction card, and three-step signal band.[3]*

The available dashboard capture was visually blank and is not used as evidence of a successful dashboard composition. Dashboard behavior is described from the implementation and test evidence instead.

## 09 AI Architecture

The AI workflow is server-side. The client calls the typed `assessment.submit` procedure through the tRPC client; the server sends structured messages to `invokeLLM` and requests strict JSON-schema output. The profile schema contains `headline`, `strengths`, `priorities`, and `confidence`; each programme reasoning request asks for one concise `reasoning` string.[2]

The model receives the assessment for profile interpretation. For reasoning, it receives the selected programme record and the assessment. The system prompts explicitly prohibit invented rankings, accreditation, deadlines, scholarships, employment outcomes, and additional requirements.[2]

The prototype has a failure-tolerant path. If the AI service is unavailable or returns unusable content, `aiJson` returns a deterministic fallback. The integration tests intentionally mock the AI service as unavailable and confirm that the assessment still returns a profile, three matches, and non-empty reasoning.[5]

The interface labels profile summaries and recommendation explanations as **AI-generated**. This makes the source of the language visible rather than presenting generated text as institutional fact.

## 10 Data & Recommendation Logic

The catalogue is a typed in-memory array of five fictional programmes. Each record includes an identifier, name, level, duration, numeric cost, display cost, requirements, tags, locations, and summary.[2]

The matching engine is deterministic. Interest tags contribute 22 points per overlap. Compatible location contributes 20 points. A programme within the assessment budget contributes 24 points; an over-budget programme loses 12. A goal containing “lead” adds 15 points for leadership programmes, and a goal containing “career” adds 8 points for technology programmes. The final score is clamped between 0 and 100.[2]

This logic intentionally separates “which programmes rise to the top” from “how the result is explained.” The result cards therefore show a score that can be traced to explicit rules, while the AI explains the fit in natural language.

The server also validates generated text before returning it. The grounding helper rejects selected unsupported claims, unsupported institution/entity language, numeric claims not found in the source text, overlong output, and output without grounding terms. If validation fails, the implementation falls back to grounded deterministic copy.[2]

This is a practical MVP guardrail, not a complete factuality evaluator. It does not prove that every semantic claim is correct, which remains a production risk and roadmap item.

## 11 Automation/API Integration

The actual implemented integration is the built-in server-side LLM helper, called through the server’s `invokeLLM` wrapper. Its credential is kept server-side; the demo documentation explicitly states that no API key is exposed to the client.[1] [2]

The application also uses the existing Manus OAuth/authentication scaffold for session and administrator gating, and typed tRPC procedures for client-server communication. These are application infrastructure integrations, not external programme or admissions APIs.[2]

No real programme catalogue API, CRM, email provider, SMS provider, admissions system, payment service, or background automation was implemented for the MVP. The lead form stores data in the server process and does not send it to a real institution.[1]

**Proposed production functionality, not implemented:** connect an authoritative catalogue source; persist leads in a database; integrate a CRM or admissions workflow; establish email/notification delivery; add admin invitation and role-management procedures; and introduce scheduled catalogue refresh or lead follow-up jobs only after their operational requirements are defined.

## 12 Testing

Testing combined static validation, automated tests, build validation, and visual review.

| Test layer | Actual evidence | Result |
|---|---|---|
| TypeScript | `pnpm check` | Passed |
| Unit behavior | Matching, grounding, catalogue shape, consent validation | Passed |
| Integration behavior | AI-unavailable assessment fallback and assessment-to-lead-to-dashboard flow | Passed |
| Authentication | Logout cookie clearing test | Passed |
| Production build | `pnpm build` | Passed |
| Visual review | Desktop and mobile landing-page layouts | Completed |

The final test run recorded three test files and eight passing tests. The build completed successfully; Vite emitted a non-blocking bundle-size advisory.[1] [5] The tests are behavior-focused and do not establish recommendation accuracy, accessibility conformance, load performance, or production security readiness.

## 13 Problems Discovered

The implementation exposed several issues that materially influenced the final prototype.

First, the initial dashboard shell contained placeholder navigation. It was replaced with valid MVP destinations for the lead overview and public assessment. Second, loading feedback needed to be explicit: the final implementation includes an assessment-processing skeleton, a dedicated results-transition skeleton, and dashboard loading skeletons.

Third, AI safety required more than a prompt. The implementation added grounded fallback behavior and source-aware checks for forbidden claims, unsupported entity language, unsupported numeric claims, and missing grounding terms. This reduced obvious hallucination paths but did not eliminate semantic factuality risk.

Fourth, the prototype’s persistence boundary became important during review. Leads are visible in the dashboard during the active server session, but they are not durable database records. The demo documentation keeps that limitation visible rather than implying a complete admissions backend.[1]

Finally, one captured dashboard screenshot was blank and was excluded from visual success evidence. The dashboard is supported by code and integration tests, but the screenshot artifact itself should not be presented as proof of a polished dashboard rendering.

## 14 Improvements

The implemented improvements focused on reliability and clarity rather than scope expansion. The public flow gained meaningful loading, empty, and error states. The assessment transition now explains that the system is reading the student’s direction instead of leaving the user on a frozen form. The dashboard gained retry behavior and an empty state that links back to the assessment.

The interface also gained persistent demo labeling and AI-generated badges in the locations where confusion would be most costly. Consent is enforced in both the UI and the server schema. The comparison control is limited to three programmes, matching the approved MVP requirement.

The recommendation path was improved by moving factual selection into deterministic code and retaining AI for interpretation and explanation. The final test suite added explicit coverage for unsupported AI claims, numeric claim rejection, AI fallback, consent rejection, consented lead creation, and the integrated workflow.[5]

## 15 Final Product

The final prototype is a coherent discovery-to-enquiry experience rather than a collection of disconnected screens. The landing page establishes the Northstar / study metaphor and starts the assessment. The assessment captures the minimum context required by the matching rules. The results page turns that context into a profile, a scored shortlist, grounded explanations, and comparison. The lead form provides a clear next action without pretending to contact a real institution.

For an admissions-facing user, the dashboard provides a protected overview of captured demo enquiries and simple programme-interest summaries. Its content model is intentionally small: total enquiries, tracked programme count, catalogue status, recent enquiries, and programme-interest bars.

The product is a validated MVP prototype. It is not an authoritative programme search engine, an admissions decision-maker, a CRM, or a production counselling service.

## 16 Limitations

The most significant limitation is the catalogue. All five entries are fictional and simulated. Their costs, requirements, locations, durations, and summaries are not evidence about real institutions.[1]

The second limitation is persistence. Lead data is kept in an in-memory server array, so it is session-bound and unsuitable for real personal-data handling. There is no durable repository, retention policy, export workflow, deletion workflow, or audit trail.

The third limitation is AI evaluation. The prototype validates structure and blocks several obvious unsupported claim classes, but it does not have a labelled evaluation dataset, human review process, confidence calibration, or semantic fact-checking service.

The fourth limitation is measurement. No user research metrics, funnel metrics, conversion rate, recommendation accuracy, latency benchmark, cost-per-assessment, or accessibility audit result was recorded. The case study therefore makes no quantitative performance claims.

The fifth limitation is integration scope. There is no real catalogue API, CRM, email, SMS, institution referral, scheduled automation, or production data pipeline. Those are proposed next steps, not implemented capabilities.

## 17 Future Roadmap

| Horizon | Proposed work | Why it matters |
|---|---|---|
| Next prototype iteration | Persist leads in the project database with consent timestamp, retention metadata, and admin audit fields | Converts the session-only demo into a durable but controlled workflow |
| Next prototype iteration | Add an authoritative, reviewed programme catalogue with provenance and update status | Replaces fictional demo data with verifiable content |
| Validation | Create an evaluation set of student profiles, expected programme attributes, and reviewed explanations | Measures recommendation consistency and grounding |
| Operations | Add admin invitation, role management, lead export, and deletion workflows | Makes dashboard use safer for real teams |
| Integration | Add CRM/email handoff only after consent and data-retention rules are approved | Connects the enquiry to a real follow-up process |
| Product | Add student history, saved shortlists, and transparent “why this matched” details | Extends value beyond a single session |
| Quality | Run accessibility, mobile-device, latency, and cost testing | Establishes production readiness evidence rather than assumptions |

The roadmap deliberately starts with data authority, persistence, governance, and evaluation before adding more AI features.

## 18 What I Learned

The most important lesson was that AI should not own the entire recommendation decision when the product has a finite catalogue and explicit user preferences. Deterministic scoring made the prototype easier to explain, test, and debug, while AI remained useful for interpretation and language.

The second lesson was that demo boundaries are part of UX. Labels such as **DEMO CATALOGUE**, **AI-generated**, and “not sent to a real institution” prevent a polished interface from creating false confidence. This is especially important when the visual quality makes a prototype feel more authoritative than it is.

The third lesson was that failure states need to be designed alongside the happy path. The AI-unavailable integration test and the loading, retry, empty, and fallback states made the demonstration more reliable without introducing a large technology footprint.

The fourth lesson was that implementation evidence is more valuable than aspirational architecture. The final case study can name the exact routes, schemas, scoring rules, tests, and limitations because they exist in the code. Production integrations and metrics remain clearly marked as future work until they are actually built and measured.

## References

[1]: ./DEMO.md "Northstar / study MVP Demo Guide"
[2]: ./server/routers.ts "Implemented tRPC procedures, catalogue, AI workflow, matching logic, lead validation, and dashboard"
[3]: ../screenshots/webdev-preview-root-1786821451862943934-1601.png "Verified landing-page screenshot"
[4]: ./client/src/index.css "Implemented visual system, responsive layout, and loading-state styles"
[5]: ./server/student-support.test.ts "Focused unit tests"
[6]: ./server/student-support.integration.test.ts "AI fallback and assessment-to-lead-to-dashboard integration tests"
[7]: ./client/src/pages/Home.tsx "Implemented public landing, assessment, results, comparison, loading, and lead-capture flow"
[8]: ./client/src/pages/Dashboard.tsx "Implemented authenticated dashboard, loading, error, empty, and summary states"

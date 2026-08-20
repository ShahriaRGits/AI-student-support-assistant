# Case Study Evidence Notes

## Verified documentation

- DEMO.md describes Northstar / study as a polished student-programme recommendation MVP.
- Public flow: landing page -> four-step assessment -> server-side AI interpretation -> deterministic scoring of five fictional demo programmes -> AI-labeled reasoning -> comparison of up to three programmes -> consented enquiry.
- Admin dashboard is available at /dashboard for authenticated administrators.
- Catalogue is fictional, simulated, and labeled DEMO CATALOGUE. It contains five entries with names, levels, durations, estimated costs, requirements, tags, and location attributes.
- Leads are stored in the server process for the MVP demonstration and are visible during the active session.
- Verification commands documented: pnpm check, pnpm test, pnpm build.
- Documentation reports successful production build with a non-blocking Vite bundle-size advisory and desktop/mobile landing-page visual verification.
- Production follow-up explicitly includes database-backed leads, authoritative catalogue data, consent/retention policies, admin invitation/role management, and recommendation evaluation datasets.

## Verified implementation

- assessmentSchema validates academicBackground, one or more interests, goals, budget enum, and location enum.
- Five fictional programmes are hard-coded in server/routers.ts.
- scoreProgram scores tag/interest overlap, location compatibility, budget fit, leadership goals, and career/technology relevance, bounded to 0-100.
- aiJson invokes the server-side built-in LLM with strict JSON schema output and returns deterministic fallback data on failure.
- isGroundedText blocks forbidden unsupported claims, unsupported institution/entity terms, unsupported numeric claims, overlong text, and text without grounding terms.
- Leads use a zod schema requiring name, valid email, phone, consent literal true, assessment, and matches; storage is in-memory.
- dashboard is admin-gated and returns demo lead data plus programme-interest summaries.
- App routes are /, /dashboard, and fallback /404.
- Home.tsx contains landing, four assessment steps, loading transition, results, comparison, and lead modal in one public workflow.
- Dashboard.tsx contains authenticated dashboard query, loading skeleton, retry error state, empty state, enquiry list, KPI cards, and programme-interest bars.
- index.css uses an editorial premium direction: Playfair Display, DM Mono, ivory/deep-green palette, orbit/path motif, card hierarchy, skeleton animation, and mobile breakpoint below 800px.

## Verified tests

- auth.logout.test.ts passes.
- student-support.test.ts passes: deterministic score comparison, forbidden/numeric AI claim rejection, catalogue shape, consent rejection, consented lead creation.
- student-support.integration.test.ts passes: fallback assessment results when AI unavailable, three matches, lead capture, admin dashboard visibility.
- Final validation recorded 3 test files and 8 passing tests; pnpm check passed; pnpm build passed.

## Visual evidence

- Landing screenshot: /home/ubuntu/screenshots/webdev-preview-root-1786821451862943934-1601.png, 1279x941. Shows Northstar/study wordmark, DEMO EXPERIENCE pill, serif editorial hero, green italic emphasis, assessment CTA, deep-green programme direction card with orbit/path lines, alignment score callout, and three-step signal band.
- Dashboard screenshot: /home/ubuntu/screenshots/webdev-preview-dashboard-1786821009810219441-8222.png, 1280x720. It rendered largely blank/white with a visible vertical boundary, so it should not be presented as evidence of a successful dashboard visual state. Use implementation evidence for dashboard behavior and describe screenshot as an unsuccessful/limited capture only if needed.

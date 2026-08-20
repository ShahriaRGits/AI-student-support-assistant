# Project TODO

## Approved MVP features

- [x] Landing page with elegant hero section, feature highlights, and assessment CTA
- [x] Multi-step assessment collecting academic background, interests, goals, budget, and location preferences
- [x] Structured AI interpretation of submitted assessment responses
- [x] Clearly labeled demo program catalogue with name, level, duration, cost, requirements, and tags
- [x] Deterministic program filtering and scoring against the interpreted student profile
- [x] Clearly labeled AI-generated recommendation reasoning for matched programs
- [x] Side-by-side comparison for up to three programs
- [x] Consent-based lead capture collecting name, email, phone number, and explicit consent
- [x] Admin dashboard showing submitted leads, assessment summaries, and program match statistics
- [x] Responsive mobile-first layout with polished typography, spacing, and interaction states
- [x] Loading skeletons, meaningful empty states, and consistent error handling on every screen
- [x] Demo data labeling visible throughout catalogue and recommendation experiences
- [x] AI output labeling visible for profile summaries and recommendation reasoning
- [x] No unsupported programme facts or invented catalogue data in AI-generated content

## Definition of done

- [x] Landing page works
- [x] Assessment works
- [x] AI interpretation works
- [x] Program matching works
- [x] Recommendation reasoning works
- [x] Comparison works
- [x] Lead capture works
- [x] Dashboard works
- [x] Error states work
- [x] Loading states work
- [x] Mobile layout works
- [x] Demo data is clearly identified
- [x] No obvious broken buttons
- [x] AI does not invent unavailable data
- [x] Core workflow has been tested
- [x] Documentation exists
- [x] Demo instructions exist

## Quality and delivery

- [x] Secure handling of server-side AI credentials
- [x] Unit and integration tests cover core matching, validation, and lead workflows
- [x] Critical and high-severity issues fixed before completion
- [x] Final acceptance checklist reviewed before checkpoint

## Follow-up verification fixes

- [x] Replace DashboardLayout placeholder navigation with real admin navigation only
- [x] Add real loading skeleton components for public assessment/results and dashboard states
- [x] Add server-side validation or constrained sanitization for AI output against supplied facts
- [x] Add tests for assessment submission, deterministic matching/scoring, AI fallback, dashboard data flow, and the core workflow

## Final acceptance review fixes

- [x] Add an explicit results loading skeleton/state for the assessment submission transition
- [x] Add fact-aware validation that checks AI output against submitted values and supplied programme fields
- [x] Add tests for assessment submission fallback, dashboard query output, and the integrated assessment-to-lead workflow

- [x] Strengthen AI fact validation with an allowlist-based unsupported-claim check before returning generated profile and reasoning text

## GitHub and localhost packaging

- [x] Add GitHub-ready repository documentation and contribution guidance
- [x] Add safe local environment template without secrets
- [x] Add localhost setup, run, test, build, and troubleshooting instructions
- [x] Add optional local database configuration guidance without changing MVP defaults
- [x] Validate the packaged project with type check, tests, and production build

- [x] Add a committed placeholder-only environment template under a non-.env filename and reference it from the setup documentation

## Reduced GitHub package

- [ ] Exclude dependencies, build output, logs, screenshots, temporary artifacts, and repository metadata from the GitHub source ZIP
- [ ] Preserve application source, tests, workflows, documentation, and localhost setup files
- [ ] Verify the reduced ZIP contents and integrity

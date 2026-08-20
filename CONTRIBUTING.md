# Contributing

Thank you for contributing to Northstar / study. This repository is an MVP prototype, so changes should preserve the explicit demo boundaries unless a feature is intentionally promoted into a separately reviewed production milestone.

## Development workflow

Create a branch for each change, install dependencies with `pnpm install`, and run the local server with `pnpm dev`. Before opening a pull request, run:

```bash
pnpm check
pnpm test
pnpm build
```

Keep secrets in local environment files only. Do not commit `.env`, API keys, OAuth credentials, personal lead data, generated logs, or screenshots that contain private information.

## Product boundaries

Do not replace the fictional programme catalogue with real institution data without documenting provenance and review status. Do not add claims about accreditation, rankings, deadlines, scholarships, employment outcomes, or requirements unless those facts come from an authoritative reviewed source. Preserve explicit consent on lead capture and keep demo labels visible while the data remains simulated.

## Pull requests

Describe the user-visible change, the implementation files touched, the tests run, and any remaining limitations. Include screenshots only when they demonstrate a verified state and contain no private information. If a change affects AI output, add or update tests for schema validity, fallback behavior, and unsupported-claim handling.

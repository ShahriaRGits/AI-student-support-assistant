# Northstar / study MVP Demo Guide

## What is implemented

Northstar / study is a polished student programme recommendation MVP. The public flow begins on the landing page, moves through a four-step assessment, interprets the answers with a server-side AI call, deterministically scores the demo catalogue, generates clearly labeled AI reasoning for each result, supports comparison of up to three programmes, and captures a consented enquiry. The admin dashboard is available at `/dashboard` for authenticated administrators.

## Demo boundaries

The programme catalogue is simulated and is labeled as **DEMO CATALOGUE** throughout the experience. It contains five fictional programme entries with names, levels, durations, estimated costs, requirements, tags, and location attributes. These entries are not institution listings and must be verified before any production use.

AI-generated profile summaries and recommendation explanations are labeled **AI-generated**. The server prompt instructs the model to use only submitted assessment data and supplied catalogue fields, and to avoid inventing rankings, accreditation, deadlines, scholarships, employment outcomes, or additional requirements. If the AI service is unavailable, the server returns a deterministic fallback profile or explanation so the core demonstration remains usable.

Lead submissions are stored in the server process for this MVP demonstration and are visible in the authenticated dashboard during the active session. The lead form requires name, email, phone, and an explicit consent checkbox. The form explicitly states that it is a demo enquiry and does not send information to a real institution.

## Suggested demonstration path

Open the public landing page and select **Begin your assessment**. Complete the four steps with an academic background, one or more interests, a goal, a budget, and a location. Select **See my matches** and wait for the AI interpretation and programme shortlist. Use the **Compare** actions on up to three cards to view the side-by-side comparison. Select **Save my shortlist** or **Connect with the team**, enter demo contact details, check the explicit consent field, and submit. Finally, open `/dashboard` while authenticated as an admin to review the captured enquiry and programme-interest summary.

## Verification commands

```bash
pnpm check
pnpm test
pnpm build
```

The current test suite covers authentication logout behavior, demo catalogue shape, consent rejection, and successful consented lead creation. Visual verification was completed for desktop and mobile landing-page layouts. The production build completes successfully; Vite reports only a non-blocking bundle-size advisory.

## Production follow-up

Before production use, replace the in-memory lead store with a database-backed repository, load a reviewed catalogue from an authoritative source, define institution-specific consent and retention policies, add admin invitation/role-management procedures, and establish evaluation datasets for recommendation quality. No API key is exposed to the client; the built-in AI credential remains server-side.

# Northstar / study

AI Student Support & Program Recommendation Assistant — a validated MVP prototype.

Northstar / study guides a prospective student from a landing page through a four-step assessment, server-side AI interpretation, deterministic matching against a clearly labeled fictional catalogue, AI-generated reasoning, comparison of up to three programmes, and consent-based demo lead capture. An authenticated dashboard exposes the session’s demo enquiries and programme-interest summary.

> **Prototype boundary:** This repository contains a demonstration product. The five-programme catalogue is fictional, lead records are stored in memory for the active server session, and the enquiry form does not contact a real institution. Do not use the demo catalogue or lead workflow for production admissions activity.

## Requirements

| Requirement | Recommended version |
|---|---|
| Node.js | 22.x |
| pnpm | 10.x |
| Git | Current stable version |
| Manus project environment | Required for the built-in authentication and server-side AI workflow |

## Local setup

Clone the repository and install dependencies:

```bash
git clone <YOUR_GITHUB_REPOSITORY_URL>
cd ai-student-support-assistant
pnpm install
```

Review [`LOCAL-ENVIRONMENT.md`](./LOCAL-ENVIRONMENT.md) and [`LOCAL-ENVIRONMENT.example.txt`](./LOCAL-ENVIRONMENT.example.txt) before starting the server. Copy the placeholder file to a local `.env` file, replace the placeholders with real project values, and never commit the resulting file. In the managed Manus workspace, the required server-side environment variables are injected automatically. In a standalone local clone, you must provide valid values for the authentication and built-in AI services or use the deterministic demo fallback where the request can proceed without a live model response.

Start the development server:

```bash
pnpm dev
```

Open the local application at [http://localhost:3000](http://localhost:3000). The public assessment is at `/`; the authenticated dashboard is at `/dashboard`.

## Verification

Run the same checks used for the validated MVP:

```bash
pnpm check
pnpm test
pnpm build
```

The test suite covers catalogue shape, deterministic scoring, AI-output guardrails, consent rejection, consented lead creation, AI-unavailable fallback behavior, and the assessment-to-lead-to-dashboard workflow. The production build is a validation step only; this repository does not claim that the prototype is production deployed.

## Demo walkthrough

1. Open the public landing page and select **Begin your assessment**.
2. Complete the four steps with academic background, at least one interest, a goal, a budget, and a location.
3. Select **See my matches** and wait for the interpretation/loading state.
4. Review the AI-labeled profile and the three deterministic programme matches.
5. Use **Compare** on up to three cards.
6. Select **Save my shortlist** or **Connect with the team**.
7. Enter demo contact details and tick the explicit consent checkbox.
8. Open `/dashboard` while authenticated as an administrator to review the session’s demo enquiry.

## GitHub upload

Create an empty repository on GitHub, then run:

```bash
git init
git add .
git commit -m "Prepare Northstar study MVP for local development"
git branch -M main
git remote add origin <YOUR_GITHUB_REPOSITORY_URL>
git push -u origin main
```

Before pushing, confirm that `.env`, `.env.local`, build output, dependency directories, logs, and project-managed metadata are ignored. Use `git status --ignored` to check the result. If a secret has ever been committed, rotate it immediately; deleting it from a later commit does not make it safe.

## Project structure

```text
client/                  React application and UI components
drizzle/                 Database schema and generated migration files
server/                  tRPC procedures, authentication, AI workflow, tests
shared/                  Shared constants and types
DEMO.md                  Demonstration boundaries and walkthrough
LOCAL-ENVIRONMENT.md     Local variable and secret setup guidance
PORTFOLIO-CASE-STUDY.md  Evidence-based portfolio case study
todo.md                  Implementation and acceptance checklist
```

## Production follow-up, not included in this MVP

Before any real student or institution use, replace the fictional catalogue with an authoritative reviewed source, persist leads in a controlled database, define consent and retention policies, add admin invitation and role-management workflows, evaluate recommendation quality against reviewed cases, and connect any CRM or notification integration only after its privacy and consent requirements are approved.

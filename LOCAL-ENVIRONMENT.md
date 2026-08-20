# Local environment setup

The application reads environment variables through the existing server configuration. Keep all real values in a local `.env` file that is ignored by Git. Do not paste credentials into source files, README files, screenshots, issue comments, or GitHub commits.

## Required categories

| Variable category | Variables | Purpose |
|---|---|---|
| Runtime | `NODE_ENV`, `PORT` | Starts the local server in development on the selected port |
| Authentication | `VITE_APP_ID`, `OAUTH_SERVER_URL`, `VITE_OAUTH_PORTAL_URL`, `JWT_SECRET` | Enables the existing Manus OAuth/session flow |
| Server-side AI | `BUILT_IN_FORGE_API_URL`, `BUILT_IN_FORGE_API_KEY` | Allows the server to request structured AI interpretation and reasoning |
| Frontend built-in API | `VITE_FRONTEND_FORGE_API_URL`, `VITE_FRONTEND_FORGE_API_KEY` | Supports the scaffold’s frontend integration where required |
| Owner metadata | `OWNER_OPEN_ID`, `OWNER_NAME` | Identifies the project owner and admin behavior in the existing scaffold |
| Application metadata | `VITE_APP_TITLE`, `VITE_APP_LOGO` | Controls application branding |
| Optional analytics | `VITE_ANALYTICS_ENDPOINT`, `VITE_ANALYTICS_WEBSITE_ID` | Enables analytics only when explicitly configured |
| Optional database | `DATABASE_URL` | Supports the scaffold’s database connection; the current MVP lead flow remains in memory |

## Local file pattern

Create a local file named `.env` at the project root and add the values supplied by your project or deployment environment. A generic shape is shown below only to document names; replace every placeholder before starting a real local session:

```dotenv
NODE_ENV=development
PORT=3000
DATABASE_URL=
VITE_APP_ID=replace_me
OAUTH_SERVER_URL=replace_me
VITE_OAUTH_PORTAL_URL=replace_me
JWT_SECRET=replace_with_a_long_random_secret
BUILT_IN_FORGE_API_URL=replace_me
BUILT_IN_FORGE_API_KEY=replace_me
VITE_FRONTEND_FORGE_API_URL=replace_me
VITE_FRONTEND_FORGE_API_KEY=replace_me
OWNER_OPEN_ID=
OWNER_NAME=
VITE_APP_TITLE=Northstar / study
VITE_APP_LOGO=
VITE_ANALYTICS_ENDPOINT=
VITE_ANALYTICS_WEBSITE_ID=
```

The values above are placeholders, not working credentials. The repository already ignores `.env` and related local environment files. Confirm with `git status` that the file is not staged.

## Local behavior without live AI

The server includes deterministic fallback profile and reasoning behavior when the AI request fails. This keeps the core demonstration available, but fallback output is not equivalent to a live model response. The catalogue remains fictional and the lead store remains session-only.

## Troubleshooting

If the app does not start, verify the Node.js and pnpm versions, run `pnpm install`, confirm that port 3000 is available, and run `pnpm check` for configuration/type errors. If authentication fails, check the OAuth variables and callback configuration supplied by the project environment. If AI requests fail, verify the server-side built-in API URL and key; do not move the key into client code. If the dashboard is empty, complete the public assessment and consented demo enquiry in the same active server session.

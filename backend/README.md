# Voxora Instant Leads API

The supplied ZIP contains one static HTML file and an image. It has no backend, no Supabase connection, no API routes, and its login was only client-side `sessionStorage`. This backend adds the missing server/API layer without redesigning the UI.

## Created

- `backend/server.js` — Express API, server-side session auth, Supabase connection, client list/read/update routes.
- `backend/package.json` — backend dependencies/scripts.
- `backend/.env.example` — required configuration placeholders.
- `backend/README.md` — setup and behavior notes.
- Existing `voxora_ai_instant_lead_admin_crm_final_v2.html` — only behavior hooks were changed so the existing login and Save Changes actions call the backend; no UI markup/styles were redesigned.

## Main endpoint

`PUT /api/instant-clients/:clientId`

The route performs an UPDATE on `instant_clients`, filtering by the existing ID. It does not insert, delete, or change the ID, and it touches only the client name, OmniDimension agent ID, and OmniDimension from-number ID columns.

## Default Supabase columns

- `id`
- `client_name`
- `omnidimension_agent_id`
- `omnidimension_from_number_id`

These are the exact column names used by the API by default. If your existing table uses different names, set the four `*_COLUMN` variables in `.env` to the real names rather than changing the frontend.

## Authentication

The supplied frontend did not contain real server-verifiable authentication. The backend therefore adds a minimal server-side login using `ADMIN_EMAIL` and `ADMIN_PASSWORD` from `.env`, with an HttpOnly session cookie. The existing login screen remains visually unchanged. The Supabase service-role key never reaches the browser.

## Run

1. `cd backend`
2. `npm install`
3. Copy `.env.example` to `.env` and fill in real values.
4. `npm start`
5. Open the supplied HTML through the backend at `http://localhost:3001/voxora_ai_instant_lead_admin_crm_final_v2.html`.

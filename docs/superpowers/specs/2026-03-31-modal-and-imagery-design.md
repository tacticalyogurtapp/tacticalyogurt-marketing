# Modal, Imagery & Backend Design
**Date:** 2026-03-31
**Status:** Approved

---

## Overview

Activate all non-functional CTA buttons on the marketing landing page by wiring them to a contact/waitlist modal. Add imagery (photos + SVG icons) to enrich content-heavy sections. Define the backend required to receive and store form submissions.

---

## 1. Modal

### Trigger Buttons

All buttons currently pointing to `href="#"` will open the modal instead:

| Button | Location | Plan passed |
|---|---|---|
| Join Early Access | Tinkerer pricing card | The Tinkerer |
| Join Early Access | Comparison table row | The Tinkerer |
| Get Notified at Launch | Operator pricing card | The Operator |
| Get Notified | Operator comparison table row | The Operator |
| Get Notified at Launch | Studio pricing card | The Studio |
| Get Notified | Studio comparison table row | The Studio |
| Join Early Access — It's Free | CTA banner | (none / generic) |

Footer links (Privacy, Terms, Contact) are out of scope for this spec.

### Modal Behaviour

- Single modal element in the HTML, shown/hidden via JS
- Opens on button click; closes on backdrop click or ✕ button
- `data-plan` attribute on each trigger button passes the plan name into the modal
- Modal title set dynamically by JS on open:
  - "The Tinkerer" → **Join Early Access — The Tinkerer**
  - "The Operator" → **Get Notified at Launch — The Operator**
  - "The Studio" → **Get Notified at Launch — The Studio**
  - No plan → **Join Early Access**
- Body scroll locked while modal is open

### Form Fields

| Field | Type | Required |
|---|---|---|
| First Name | text input | Yes |
| Last Name | text input | Yes |
| Email | email input | Yes |
| Business Name | text input | No |
| Reason | dropdown (grouped) | No |
| Message | textarea | No |
| Plan | hidden input | Auto-filled from trigger |

**Reason dropdown groups:**

- *Sales:* Interested in a paid plan · Want a demo · Pricing question
- *Support:* Need help with setup · Found a bug · Feature request
- *General:* Just checking it out · Other

### Form States

1. **Idle** — form ready, submit button active
2. **Submitting** — submit button disabled, spinner shown, inputs locked
3. **Success** — form replaced with thank-you message, close button visible
4. **Error** — inline error message shown below submit button, form stays editable

### Submission

- `POST /api/contact` (URL configured as a JS constant at top of script block for easy swap)
- Request body (JSON): `{ firstName, lastName, email, businessName, reason, message, plan }`
- On `2xx`: show success state
- On network error or non-2xx: show error state with message

### Styling

- Matches existing dark theme: `--card` background, `--border` border, `--blue` primary button
- Backdrop: `rgba(0,0,0,0.6)` with `backdrop-filter: blur(4px)`
- Modal max-width: `480px`, centered, `border-radius: 12px`
- First Name / Last Name displayed side-by-side on desktop, stacked on mobile
- Same font stack as rest of page (`--sans` for labels, `--mono` for small helper text)

---

## 2. Imagery

### New Photo Breaks

Two new full-width photo sections using the existing `photo-break` CSS component:

| Position | Between sections | Image subject | Overlay text |
|---|---|---|---|
| Photo Break 2 | Features → Integrations | Filament spool rack / filament wall | "Every spool. Every color. Every gram." |
| Photo Break 3 | How it Works → Pricing | Workbench with printers running | "Set it up once. Let it run." |

Images sourced from Unsplash (same pattern as existing photo breaks). `onerror` fallback to a second Unsplash URL as already done on the page.

### Feature Category Icons

Replace emoji in `.cat-icon` divs with inline SVGs (24×24, stroke-based, `currentColor`). Existing colored `background` on each `.cat-icon` is preserved.

| Category | Icon |
|---|---|
| Inventory Management | Layered box / package |
| Printer Fleet Management | Printer outline |
| Print Job Workflow | Gear / cog |
| Print File Management | File with stacked layers |
| Orders & Customer Management | Shopping bag |
| Tasks, Markets & Subscriptions | Checklist / clipboard |

All SVGs inline — no external icon library dependency.

---

## 3. Backend Requirements

### API Endpoint

```
POST /api/contact
Content-Type: application/json

{
  "firstName": "string (required)",
  "lastName": "string (required)",
  "email": "string (required, valid email)",
  "businessName": "string (optional)",
  "reason": "string (optional)",
  "message": "string (optional)",
  "plan": "string (optional)"
}
```

**Response:**
- `200 { success: true }` — submission saved
- `400 { error: "Validation message" }` — missing required fields or invalid email
- `500 { error: "Internal error" }` — unexpected failure

### Data Storage

**Supabase (free tier)** — Postgres database.

Table: `submissions`

| Column | Type | Notes |
|---|---|---|
| id | uuid | Primary key, auto-generated |
| first_name | text | Required |
| last_name | text | Required |
| email | text | Required |
| business_name | text | Nullable |
| reason | text | Nullable |
| message | text | Nullable |
| plan | text | Nullable |
| created_at | timestamptz | Default: `now()` |

### Notifications

- **Team notification:** Email to TacticalYogurt team on every submission via **Resend** (free tier: 3,000 emails/month)
- **Subscriber confirmation:** Optional — reply-to email confirming they're on the list

### Hosting

**Vercel (free Hobby plan)** — serverless function at `/api/contact.js`. Deploys automatically on push to `main`.

The marketing page remains static on GitHub Pages and calls the Vercel API URL (configured as a JS constant).

### Recommended Stack

| Layer | Service | Cost |
|---|---|---|
| API / serverless | Vercel | Free |
| Database | Supabase | Free |
| Email | Resend | Free (3k/mo) |

All three connect to GitHub for automatic deploys. No ops overhead. Upgrade paths available on all three when needed.

---

## Out of Scope

- Footer links (Privacy, Terms, Contact) — separate task
- Actual paid plan billing / Stripe integration
- User authentication
- Admin dashboard to view submissions (use Supabase dashboard directly for now)

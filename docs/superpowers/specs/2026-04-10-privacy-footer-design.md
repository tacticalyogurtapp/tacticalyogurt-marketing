# Privacy Policy — Expandable Footer Section

**Date:** 2026-04-10
**Status:** Approved

---

## Overview

Add a privacy policy to the TacticalYogurt marketing site as an expandable panel that slides up from the footer when the "Privacy" link is clicked. No new pages, no modal overlay — everything stays on the single-page site.

---

## Content

### Policy text (Standard tier)

**Privacy Policy**
*Last updated: April 10, 2026*

> The short version: We collect only what we need to run TacticalYogurt. We don't sell your data. We don't spam you.

**What we collect**

*On this website (marketing & waitlist):*
We collect your name, email address, and optionally the number of printers you run when you fill out our interest form. No tracking scripts, no ad pixels, no cookies set by us.

*In the app:*
To run your account we collect your name, email, and encrypted password (or OAuth token if you sign in with Google, Microsoft, or Apple). The app also stores the business data you enter — filament inventory, printer records, print jobs, orders, customers, parts, uploaded 3D model files, and data synced from e-commerce platforms you connect (Shopify, Etsy, WooCommerce, Square, Patreon). We store only what you put in.

**How we use it**
- To send you early access updates and product announcements (waitlist)
- To operate your account and deliver the service (app)
- To send transactional emails — invitations, password resets, welcome messages
- To notify us internally when a new farm is created (admin alert only)

We do not use your data for advertising. We do not sell or share it with third parties for their own purposes.

**Third-party services**

| Service | Purpose | Data shared |
|---|---|---|
| Resend | Email delivery | Your email address, email content |
| Cloudflare R2 / AWS S3 | File storage | Uploaded 3D model files |
| Google / Microsoft / Apple | Optional sign-in | OAuth token only |
| Shopify, Etsy, Square, WooCommerce, Patreon | E-commerce sync (only if you connect them) | OAuth token + synced order/product data |

These services process data on our behalf. We do not authorize them to use your data for their own purposes.

**Data storage and security**
Your data is stored on servers we control, hosted in the United States. Passwords are hashed using bcrypt and never stored in plaintext. OAuth tokens from e-commerce integrations are encrypted at rest. We use HTTPS for all data in transit.

**Data retention**
We keep your data for as long as your account is active. If you request deletion, we will remove your personal data within 30 days. Waitlist-only submissions (no account) are kept until you ask us to remove them or until we launch.

**Your rights**
You can ask us to:
- Confirm what data we hold about you
- Correct inaccurate information
- Delete your data entirely
- Remove you from the waitlist

Email us at **tacticalyogurt@gmail.com** and we'll respond within 5 business days.

**Contact**
TacticalYogurt — tacticalyogurt@gmail.com

---

## Architecture

### Trigger

The existing `<a href="#">Privacy</a>` link in the footer is updated to call a `togglePrivacy()` JavaScript function. No page navigation occurs.

### Panel structure

A `<div id="privacyPanel">` is inserted in the HTML between the main page content and the `<footer>` element. It is hidden by default (`max-height: 0`, `overflow: hidden`) and expands via CSS transition when an `.open` class is toggled.

```
[page content]
[#privacyPanel]   ← expands/collapses here
[footer]
```

### Styling

- Background: `var(--card)` — matches existing dark card theme
- Border-top: `1px solid var(--border)`
- Content constrained to `max-width: 860px`, centered with `margin: 0 auto`
- Headings use existing `--display` font and `--text` color
- Table uses `--border` for cell borders, `--muted` for header text
- Close button (✕) fixed to top-right of panel, same style as `.modal-close`
- Smooth expand: `max-height` transition, `0.3s ease`

### Behavior

- Clicking "Privacy" in footer: panel opens, footer link gains `.active` style (color: `var(--text)`)
- Clicking "Privacy" again, or the ✕ button: panel closes
- Panel does not interfere with the modal (contact form) — both can coexist independently
- No scroll-to behavior needed; the footer is at the bottom of the page so the panel naturally appears above it when expanded

### JavaScript

Single `togglePrivacy()` function:
- Toggles `.open` class on `#privacyPanel`
- Toggles `.active` class on the Privacy footer link
- No dependencies, no libraries

---

## Out of scope

- Terms of Service page (separate effort)
- Cookie consent banner (no cookies currently set by the site)
- GDPR consent flows (no EU-specific targeting at launch)
- Contact form backend (separate pinned effort)

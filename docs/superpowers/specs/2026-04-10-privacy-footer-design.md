# Privacy Policy & Terms of Service — Expandable Footer Panels

**Date:** 2026-04-10
**Status:** Approved

---

## Overview

Add a Privacy Policy and Terms of Service to the TacticalYogurt marketing site as expandable panels that slide up from the footer when their respective footer links are clicked. No new pages, no modal overlays — everything stays on the single-page site. Both panels share the same behavior and visual style.

---

## Content

### Privacy Policy

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

Email us at **tacticalyogurt@gmail.com** and we'll respond as soon as possible.

**Contact**
TacticalYogurt — tacticalyogurt@gmail.com

---

### Terms of Service

**Terms of Service**
*Last updated: April 10, 2026*

> The short version: Use TacticalYogurt for its intended purpose, be honest about your information, and don't do anything illegal. Your data is yours.

**Acceptance of terms**
By accessing this website or using the TacticalYogurt app, you agree to these Terms of Service. If you don't agree, please don't use the service. Signing up for the waitlist or creating an account constitutes acceptance.

**Description of service**
TacticalYogurt is a print farm management platform that helps 3D printing businesses track filament inventory, printers, print jobs, orders, customers, and e-commerce integrations. The service is currently in early access and features may change, be added, or be removed without notice.

**Your account**
You are responsible for keeping your login credentials secure and for all activity that occurs under your account. You must provide accurate information when signing up. You may not share your account with others or create accounts on behalf of someone else without their permission.

**Acceptable use**
You agree not to:
- Use the service for any unlawful purpose
- Attempt to gain unauthorized access to any part of the service or its infrastructure
- Upload malicious files or code
- Scrape, reverse-engineer, or copy the service for competitive purposes
- Impersonate another person or organization

**Your data**
You own the data you put into TacticalYogurt. We store it to provide the service and do not claim ownership over it. You can request a copy or deletion of your data at any time by emailing us. See our Privacy Policy for details on how we handle your data.

**Intellectual property**
The TacticalYogurt name, logo, app design, and underlying software are owned by TacticalYogurt. Nothing in these terms transfers any IP rights to you. You may not use our branding without written permission.

**Early access**
The service is provided in an early access state. This means:
- Features are subject to change or removal
- We cannot guarantee uninterrupted availability
- Pricing shown on this site is indicative and may change before launch
- We will make reasonable efforts to communicate significant changes in advance

**Disclaimer of warranties**
The service is provided "as is" without warranties of any kind, express or implied. We do not warrant that the service will be error-free, uninterrupted, or meet your specific requirements.

**Limitation of liability**
To the extent permitted by law, TacticalYogurt shall not be liable for any indirect, incidental, or consequential damages arising from your use of the service, including loss of data or business interruption.

**Termination**
We may suspend or terminate your access at any time if you violate these terms. You may cancel your account at any time by contacting us. Upon termination, we will delete your data per our data retention policy.

**Changes to these terms**
We may update these terms from time to time. When we do, we will update the date at the top of this page. Continued use of the service after changes constitutes acceptance of the updated terms.

**Governing law**
These terms are governed by the laws of the United States. Any disputes shall be resolved in the jurisdiction where TacticalYogurt operates.

**Contact**
TacticalYogurt — tacticalyogurt@gmail.com

---

## Architecture

### Panel structure

Two panels are inserted in the HTML between the main page content and the `<footer>` element, one for each policy. Both are hidden by default and expand via CSS transition when triggered.

```
[page content]
[#privacyPanel]   ← expands when Privacy clicked
[#termsPanel]     ← expands when Terms clicked
[footer]
```

Opening one panel closes the other — only one is visible at a time.

### Trigger

The existing footer links are updated to call toggle functions instead of navigating:
- `<a href="#">Privacy</a>` → `onclick="togglePanel('privacy')"`
- `<a href="#">Terms</a>` → `onclick="togglePanel('terms')"`

### Styling

- Background: `var(--card)` — matches existing dark card theme
- Border-top: `1px solid var(--border)`
- Content constrained to `max-width: 860px`, centered with `margin: 0 auto`
- Headings use existing `--display` font and `--text` color
- Table uses `--border` for cell borders, `--muted` for header text
- Close button (✕) top-right of each panel, same style as `.modal-close`
- Smooth expand: `max-height` transition, `0.3s ease`
- Active footer link: `color: var(--text)` while its panel is open

### Behavior

- Clicking a footer link opens its panel and closes the other if open
- Clicking the active footer link again, or the ✕ button, closes the panel
- Panels do not interfere with the contact form modal
- Page scrolls to the panel on open so users see it without having to scroll manually

### JavaScript

Single `togglePanel(name)` function handles both panels:
- Accepts `'privacy'` or `'terms'`
- Closes whichever panel is currently open (if different from the clicked one)
- Toggles `.open` on the target panel
- Toggles `.active` on the corresponding footer link
- Scrolls panel into view on open
- No dependencies, no libraries

---

## Out of scope

- Cookie consent banner (no cookies currently set by the site)
- GDPR consent flows (no EU-specific targeting at launch)
- Contact form backend (separate pinned effort)

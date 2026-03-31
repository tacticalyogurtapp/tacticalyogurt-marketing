# Google Forms Modal Pivot
**Date:** 2026-03-31
**Status:** Approved
**Supersedes:** Sections 1 (Modal) and 3 (Backend Requirements) of `2026-03-31-modal-and-imagery-design.md`

---

## Overview

Replace the custom contact form modal and planned backend (Vercel/Supabase/Resend) with an embedded Google Form. The modal overlay and interaction pattern are preserved; the form fields, submission JS, and all backend work are dropped.

Business inquiries will be handled by a separate page (out of scope here).

---

## Modal Design

### Behaviour
- Opens on any CTA button click — all buttons call `openModal()` with no arguments
- Closes on: backdrop click, ✕ button, or Escape key
- Body scroll locked while modal is open
- No plan-aware title or subtitle — modal contains only the close button and the iframe

### Structure
```
.modal-backdrop (fixed overlay, blur backdrop)
  └── .modal (max-width: 660px, scrollable)
        ├── .modal-close button (✕, top-right)
        └── <iframe> (Google Form, width: 100%, height: 955px)
```

### Iframe
- **src:** `https://docs.google.com/forms/d/e/1FAIpQLSeQht3YLPA9Na92ew4G0Y8GVSEchCRmosn1RJxhjBrqc6bWug/viewform?embedded=true`
- **width:** `100%`
- **height:** `955px`
- **frameborder:** `0`
- Fallback text: `Loading…`

### Sizing
- Modal max-width: `660px` (widened from original 480px to better fit Google Form at native width)
- Modal max-height: `90vh`, `overflow-y: auto` (modal body scrolls on short viewports)
- Centered on screen with `backdrop-filter: blur(4px)`

---

## What Is Removed vs Original Design

| Original | Status |
|---|---|
| Custom form fields (name, email, business, reason, message) | **Removed** |
| Plan-aware modal title | **Removed** |
| Form states (idle, submitting, success, error) | **Removed** |
| Form submission JS + `API_URL` constant | **Removed** |
| Vercel serverless function `/api/contact` | **Removed** |
| Supabase database | **Removed** |
| Resend email notifications | **Removed** |

---

## What Is Unchanged

- Modal overlay, backdrop, close button, Escape/backdrop-click to close
- All 7 CTA buttons open the modal (plan argument dropped, all call `openModal()`)
- Tasks 1–3 from original plan (SVG icons, two photo breaks) — unaffected

---

## Out of Scope

- Business inquiry page (separate task)
- Footer links (Privacy, Terms, Contact)

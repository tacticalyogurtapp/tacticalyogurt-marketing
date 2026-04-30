# Contact Page Design Spec
**Project:** TacticalYogurt Marketing Site
**Date:** 2026-04-29

---

## Overview

Create a dedicated `contact.html` page that consolidates social links, contact email addresses, and the waitlist Google Form. Update `index.html` to route all "Contact Us" and "Join the Waitlist" / "Get Notified" buttons to the new page instead of opening the modal.

---

## 1. Backup

Before any changes to `index.html`, copy it to `index.backup.html` in the same directory. This is the rollback target if anything breaks.

---

## 2. New Page — `contact.html`

### 2.1 Nav
Identical to `index.html`. Same links, same "Log In" and "Get Started" buttons. No changes.

### 2.2 Hero Section
- Small, centered, full-width section
- Headline: **"Get in Touch"**
- Subtext: "Reach out on social or drop us a line — we'll get back to you soon."
- Consistent with the existing page hero style (dark background, centered text, same font stack)

### 2.3 Contact Cards
Three cards in a horizontal row, stacking to a single column on mobile. Each card links to its respective destination and uses the violet→orange gradient (`#7c3aed` → `#ea580c`) on the icon and top border accent. No glow effects.

| Card | Icon | Label | Sub-label | Link |
|---|---|---|---|---|
| Instagram | Instagram SVG | Follow Us | @tacticalyogurt | `https://www.instagram.com/tacticalyogurt` |
| Sales | Envelope SVG | Sales Inquiry | sales@tacticalyogurt.com | `mailto:sales@tacticalyogurt.com` |
| Support | Envelope SVG | Get Support | support@tacticalyogurt.com | `mailto:support@tacticalyogurt.com` |

Card style: dark card background (`var(--card)`), 2px gradient top border, icon in gradient color, label in primary text, sub-label in muted text. Subtle hover lift (`translateY(-3px)`) matching the site's existing card hover behavior.

### 2.4 Waitlist Form
- Section heading: **"Join the Waitlist"**
- Google Form embed — same iframe src as the current modal:
  `https://docs.google.com/forms/d/e/1FAIpQLSeQht3YLPA9Na92ew4G0Y8GVSEchCRmosn1RJxhjBrqc6bWug/viewform?embedded=true`
- Full-width, centered, consistent padding with the rest of the page

### 2.5 Footer
Identical to `index.html`. Same links, same social icons, same copyright.

---

## 3. Changes to `index.html`

### 3.1 Nav buttons
| Element | Current behavior | New behavior |
|---|---|---|
| "Contact Us" (desktop nav) | `onclick="openModal()"` | `href="contact.html"`, remove onclick |
| "Contact Us" (mobile nav) | `onclick="closeMenu(); openModal()"` | `href="contact.html"`, remove onclick |

### 3.2 CTA buttons throughout page
All buttons with `onclick="openModal()"` or `onclick="event.preventDefault(); openModal()"` that use "Join the Waitlist" or "Get Notified" label text:
- Change `href="#"` to `href="contact.html"`
- Remove `onclick` handler
- Keep button styles unchanged

### 3.3 Modal
Leave the modal HTML intact. Do not remove it. This preserves a clean rollback path — if needed, reverting the button hrefs restores full original behavior.

---

## 4. Files Changed

| File | Change |
|---|---|
| `index.backup.html` | New file — copy of `index.html` before changes |
| `contact.html` | New file — full contact page |
| `index.html` | Button href/onclick updates only |

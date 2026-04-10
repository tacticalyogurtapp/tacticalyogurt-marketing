# Privacy & Terms Footer Panels Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Add expandable Privacy Policy and Terms of Service panels that slide up from the footer when their respective footer links are clicked.

**Architecture:** All changes are confined to `index.html` — the single-file static site. CSS is added inline in the `<style>` block, HTML panels are inserted before the `<footer>` element, footer links are updated with `onclick` handlers, and a `togglePanel()` function is added to the existing `<script>` block. No build tools, no dependencies.

**Tech Stack:** Vanilla HTML, CSS (custom properties already defined in the file), vanilla JavaScript.

---

## File Map

| File | Action | What changes |
|---|---|---|
| `index.html` | Modify | CSS: panel styles appended after modal CSS (~line 468) |
| `index.html` | Modify | HTML: two panel divs inserted before `<!-- FOOTER -->` (~line 1419) |
| `index.html` | Modify | HTML: footer links updated with `id` and `onclick` (~lines 1424–1425) |
| `index.html` | Modify | JS: `togglePanel()` added to `<script>` block (~line 1486) |

---

### Task 1: Add CSS for the footer panels

**Files:**
- Modify: `index.html` — `<style>` block, after the line `.modal iframe { display: block; width: 100%; border: none; border-radius: 4px; }`

- [ ] **Step 1: Locate the insertion point**

Search for this exact line in the `<style>` block:
```
.modal iframe { display: block; width: 100%; border: none; border-radius: 4px; }
```

- [ ] **Step 2: Insert the footer panel CSS immediately after that line**

```css
  /* FOOTER PANELS */
  .footer-panel { max-height: 0; overflow: hidden; transition: max-height 0.35s ease; background: var(--card); border-top: 1px solid var(--border); }
  .footer-panel.open { max-height: 3000px; }
  .footer-panel-inner { max-width: 860px; margin: 0 auto; padding: 3rem 2rem 3.5rem; position: relative; }
  .footer-panel-close { position: absolute; top: 1.5rem; right: 1.5rem; background: none; border: none; cursor: pointer; color: var(--muted); font-size: 1.25rem; line-height: 1; padding: .25rem .5rem; border-radius: 4px; transition: color .2s; }
  .footer-panel-close:hover { color: var(--text); }
  .footer-panel h2 { font-family: var(--display); font-size: 1.4rem; font-weight: 600; margin-bottom: .4rem; color: var(--text); }
  .footer-panel .panel-date { font-size: .78rem; color: var(--muted); margin-bottom: 1.75rem; display: block; }
  .footer-panel h3 { font-family: var(--display); font-size: .95rem; font-weight: 600; margin: 1.75rem 0 .5rem; color: var(--text); }
  .footer-panel p { color: var(--muted); font-size: .875rem; line-height: 1.75; margin-bottom: .75rem; }
  .footer-panel ul { padding-left: 1.25rem; margin-bottom: 1rem; }
  .footer-panel ul li { color: var(--muted); font-size: .875rem; line-height: 1.75; margin-bottom: .25rem; }
  .footer-panel blockquote { border-left: 3px solid var(--blue); padding: .25rem 0 .25rem 1rem; margin: 0 0 1.25rem; }
  .footer-panel blockquote p { margin-bottom: 0; font-style: italic; }
  .footer-panel table { width: 100%; border-collapse: collapse; margin: 1rem 0 1.5rem; font-size: .825rem; }
  .footer-panel th { color: var(--muted); text-align: left; padding: .5rem .75rem; border-bottom: 1px solid var(--border); font-weight: 500; font-size: .775rem; text-transform: uppercase; letter-spacing: .04em; }
  .footer-panel td { color: var(--text); padding: .5rem .75rem; border-bottom: 1px solid rgba(255,255,255,.04); vertical-align: top; }
  .footer-panel td:first-child { white-space: nowrap; font-weight: 500; }
  .footer-links a.active { color: var(--text); }
```

- [ ] **Step 3: Open `index.html` in a browser and verify no visual change**

The panels don't exist in the DOM yet so nothing should look different. This confirms the CSS loaded without syntax errors.

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add footer panel CSS"
```

---

### Task 2: Add the Privacy Policy panel HTML

**Files:**
- Modify: `index.html` — insert before the `<!-- FOOTER -->` comment

- [ ] **Step 1: Locate the insertion point**

Find this exact comment in `index.html`:
```html
<!-- FOOTER -->
```

- [ ] **Step 2: Insert the Privacy panel HTML immediately before that comment**

```html
<!-- PRIVACY PANEL -->
<div class="footer-panel" id="privacyPanel">
  <div class="footer-panel-inner">
    <button class="footer-panel-close" onclick="togglePanel('privacy')" aria-label="Close">✕</button>
    <h2>Privacy Policy</h2>
    <span class="panel-date">Last updated: April 10, 2026</span>
    <blockquote><p>The short version: We collect only what we need to run TacticalYogurt. We don't sell your data. We don't spam you.</p></blockquote>

    <h3>What we collect</h3>
    <p><em>On this website (marketing &amp; waitlist):</em><br>
    We collect your name, email address, and optionally the number of printers you run when you fill out our interest form. No tracking scripts, no ad pixels, no cookies set by us.</p>
    <p><em>In the app:</em><br>
    To run your account we collect your name, email, and encrypted password (or OAuth token if you sign in with Google, Microsoft, or Apple). The app also stores the business data you enter — filament inventory, printer records, print jobs, orders, customers, parts, uploaded 3D model files, and data synced from e-commerce platforms you connect (Shopify, Etsy, WooCommerce, Square, Patreon). We store only what you put in.</p>

    <h3>How we use it</h3>
    <ul>
      <li>To send you early access updates and product announcements (waitlist)</li>
      <li>To operate your account and deliver the service (app)</li>
      <li>To send transactional emails — invitations, password resets, welcome messages</li>
      <li>To notify us internally when a new farm is created (admin alert only)</li>
    </ul>
    <p>We do not use your data for advertising. We do not sell or share it with third parties for their own purposes.</p>

    <h3>Third-party services</h3>
    <table>
      <thead><tr><th>Service</th><th>Purpose</th><th>Data shared</th></tr></thead>
      <tbody>
        <tr><td>Resend</td><td>Email delivery</td><td>Your email address, email content</td></tr>
        <tr><td>Cloudflare R2 / AWS S3</td><td>File storage</td><td>Uploaded 3D model files</td></tr>
        <tr><td>Google / Microsoft / Apple</td><td>Optional sign-in</td><td>OAuth token only</td></tr>
        <tr><td>Shopify, Etsy, Square, WooCommerce, Patreon</td><td>E-commerce sync (only if you connect them)</td><td>OAuth token + synced order/product data</td></tr>
      </tbody>
    </table>
    <p>These services process data on our behalf. We do not authorize them to use your data for their own purposes.</p>

    <h3>Data storage and security</h3>
    <p>Your data is stored on servers we control, hosted in the United States. Passwords are hashed using bcrypt and never stored in plaintext. OAuth tokens from e-commerce integrations are encrypted at rest. We use HTTPS for all data in transit.</p>

    <h3>Data retention</h3>
    <p>We keep your data for as long as your account is active. If you request deletion, we will remove your personal data within 30 days. Waitlist-only submissions (no account) are kept until you ask us to remove them or until we launch.</p>

    <h3>Your rights</h3>
    <p>You can ask us to:</p>
    <ul>
      <li>Confirm what data we hold about you</li>
      <li>Correct inaccurate information</li>
      <li>Delete your data entirely</li>
      <li>Remove you from the waitlist</li>
    </ul>
    <p>Email us at <strong>tacticalyogurt@gmail.com</strong> and we'll respond as soon as possible.</p>

    <h3>Contact</h3>
    <p>TacticalYogurt — <strong>tacticalyogurt@gmail.com</strong></p>
  </div>
</div>

```

- [ ] **Step 3: Open `index.html` in a browser and verify the panel is invisible**

The panel exists in the DOM but `max-height: 0` keeps it hidden. The footer should look unchanged.

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add privacy policy panel HTML"
```

---

### Task 3: Add the Terms of Service panel HTML

**Files:**
- Modify: `index.html` — insert between the privacy panel and `<!-- FOOTER -->`

- [ ] **Step 1: Locate the insertion point**

Find the `<!-- FOOTER -->` comment (it now follows the privacy panel from Task 2).

- [ ] **Step 2: Insert the Terms panel HTML immediately before `<!-- FOOTER -->`**

```html
<!-- TERMS PANEL -->
<div class="footer-panel" id="termsPanel">
  <div class="footer-panel-inner">
    <button class="footer-panel-close" onclick="togglePanel('terms')" aria-label="Close">✕</button>
    <h2>Terms of Service</h2>
    <span class="panel-date">Last updated: April 10, 2026</span>
    <blockquote><p>The short version: Use TacticalYogurt for its intended purpose, be honest about your information, and don't do anything illegal. Your data is yours.</p></blockquote>

    <h3>Acceptance of terms</h3>
    <p>By accessing this website or using the TacticalYogurt app, you agree to these Terms of Service. If you don't agree, please don't use the service. Signing up for the waitlist or creating an account constitutes acceptance.</p>

    <h3>Description of service</h3>
    <p>TacticalYogurt is a print farm management platform that helps 3D printing businesses track filament inventory, printers, print jobs, orders, customers, and e-commerce integrations. The service is currently in early access and features may change, be added, or be removed without notice.</p>

    <h3>Your account</h3>
    <p>You are responsible for keeping your login credentials secure and for all activity that occurs under your account. You must provide accurate information when signing up. You may not share your account with others or create accounts on behalf of someone else without their permission.</p>

    <h3>Acceptable use</h3>
    <p>You agree not to:</p>
    <ul>
      <li>Use the service for any unlawful purpose</li>
      <li>Attempt to gain unauthorized access to any part of the service or its infrastructure</li>
      <li>Upload malicious files or code</li>
      <li>Scrape, reverse-engineer, or copy the service for competitive purposes</li>
      <li>Impersonate another person or organization</li>
    </ul>

    <h3>Your data</h3>
    <p>You own the data you put into TacticalYogurt. We store it to provide the service and do not claim ownership over it. You can request a copy or deletion of your data at any time by emailing us. See our Privacy Policy for details on how we handle your data.</p>

    <h3>Intellectual property</h3>
    <p>The TacticalYogurt name, logo, app design, and underlying software are owned by TacticalYogurt. Nothing in these terms transfers any IP rights to you. You may not use our branding without written permission.</p>

    <h3>Early access</h3>
    <p>The service is provided in an early access state. This means:</p>
    <ul>
      <li>Features are subject to change or removal</li>
      <li>We cannot guarantee uninterrupted availability</li>
      <li>Pricing shown on this site is indicative and may change before launch</li>
      <li>We will make reasonable efforts to communicate significant changes in advance</li>
    </ul>

    <h3>Disclaimer of warranties</h3>
    <p>The service is provided "as is" without warranties of any kind, express or implied. We do not warrant that the service will be error-free, uninterrupted, or meet your specific requirements.</p>

    <h3>Limitation of liability</h3>
    <p>To the extent permitted by law, TacticalYogurt shall not be liable for any indirect, incidental, or consequential damages arising from your use of the service, including loss of data or business interruption.</p>

    <h3>Termination</h3>
    <p>We may suspend or terminate your access at any time if you violate these terms. You may cancel your account at any time by contacting us. Upon termination, we will delete your data per our data retention policy.</p>

    <h3>Changes to these terms</h3>
    <p>We may update these terms from time to time. When we do, we will update the date at the top of this page. Continued use of the service after changes constitutes acceptance of the updated terms.</p>

    <h3>Governing law</h3>
    <p>These terms are governed by the laws of the United States. Any disputes shall be resolved in the jurisdiction where TacticalYogurt operates.</p>

    <h3>Contact</h3>
    <p>TacticalYogurt — <strong>tacticalyogurt@gmail.com</strong></p>
  </div>
</div>

```

- [ ] **Step 3: Open `index.html` in a browser and verify the panel is invisible**

Footer should still look unchanged. Both panels are in the DOM but hidden.

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: add terms of service panel HTML"
```

---

### Task 4: Update footer links with IDs and onclick handlers

**Files:**
- Modify: `index.html` — footer `<ul class="footer-links">` (~line 1423)

- [ ] **Step 1: Locate the footer links**

Find this block in `index.html`:
```html
  <ul class="footer-links">
    <li><a href="#">Privacy</a></li>
    <li><a href="#">Terms</a></li>
    <li><a href="#">Contact</a></li>
  </ul>
```

- [ ] **Step 2: Replace it with**

```html
  <ul class="footer-links">
    <li><a href="#" id="privacyLink" onclick="event.preventDefault(); togglePanel('privacy')">Privacy</a></li>
    <li><a href="#" id="termsLink" onclick="event.preventDefault(); togglePanel('terms')">Terms</a></li>
    <li><a href="#">Contact</a></li>
  </ul>
```

- [ ] **Step 3: Open `index.html` in a browser and click "Privacy"**

The link click should not navigate (no `#` jump). The panel won't open yet because `togglePanel` doesn't exist — a console error is expected at this point. That's fine.

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: wire footer links to togglePanel"
```

---

### Task 5: Add the togglePanel JavaScript function

**Files:**
- Modify: `index.html` — `<script>` block, after the `handleBackdropClick` function and before the cycling headline code

- [ ] **Step 1: Locate the insertion point**

Find this line in the `<script>` block:
```javascript
  // Cycling headline
```

- [ ] **Step 2: Insert `togglePanel` immediately before that comment**

```javascript
  // Footer panels
  function togglePanel(name) {
    var panels = { privacy: document.getElementById('privacyPanel'), terms: document.getElementById('termsPanel') };
    var links = { privacy: document.getElementById('privacyLink'), terms: document.getElementById('termsLink') };
    var panel = panels[name];
    var link = links[name];
    var isOpen = panel.classList.contains('open');

    // Close all panels and deactivate all links
    Object.values(panels).forEach(function(p) { p.classList.remove('open'); });
    Object.values(links).forEach(function(l) { l.classList.remove('active'); });

    // If panel was closed, open it
    if (!isOpen) {
      panel.classList.add('open');
      link.classList.add('active');
      setTimeout(function() { panel.scrollIntoView({ behavior: 'smooth', block: 'start' }); }, 50);
    }
  }

```

The `setTimeout` delay gives the CSS transition a moment to begin before scrolling, producing a smoother feel.

- [ ] **Step 3: Open `index.html` in a browser and test Privacy**

- Click "Privacy" in the footer — panel should slide open and scroll into view
- Footer "Privacy" link should become brighter (`.active` state)
- Click "Privacy" again — panel should collapse, link should dim

- [ ] **Step 4: Test Terms**

- Click "Terms" in the footer — Terms panel should slide open
- Click "Privacy" while Terms is open — Terms should close and Privacy should open
- Click the ✕ button — panel should close

- [ ] **Step 5: Test Escape key does not close panels**

The existing `keydown` listener only closes the modal — panels are unaffected. Verify this by opening a panel and pressing Escape: the panel should stay open.

- [ ] **Step 6: Test modal coexistence**

Open the contact modal (click "Contact Us" in nav), then close it. Open a footer panel. Verify both work independently with no visual or JS conflicts.

- [ ] **Step 7: Commit**

```bash
git add index.html
git commit -m "feat: add togglePanel JS for privacy and terms footer panels"
```

---

### Task 6: Final visual check and cleanup

- [ ] **Step 1: Verify responsive behavior on narrow viewport**

Resize the browser to ~375px wide (mobile). Open each panel and confirm:
- Text is readable (no overflow)
- Table scrolls horizontally if needed (overflow is handled by `overflow: hidden` on the panel, table should wrap gracefully at `.825rem` font size)
- Close button is reachable

- [ ] **Step 2: Check footer link spacing**

With the `.active` CSS applied (`color: var(--text)`), the active link should be visually distinct but not cause any layout shift. Confirm the footer looks correct in both active and inactive states.

- [ ] **Step 3: Commit final state**

```bash
git add index.html
git commit -m "feat: privacy and terms footer panels complete"
```

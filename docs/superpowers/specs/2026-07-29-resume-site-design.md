# Resume Website — Design Spec

Date: 2026-07-29

## Purpose

A personal resume website for Jesaiah Calderon, hosted for free on GitHub Pages at
`https://jesaiahcal.github.io`, presenting his IT Support / aspiring cybersecurity
background to recruiters and hiring managers.

## Source Content

Pulled from `~/Desktop/Jesaiah Calderon Resume .docx`:

- Name: Jesaiah Calderon
- Title: IT Support Technician | Aspiring Cybersecurity Professional
- Location: Anaheim, California
- Email: jesaiah.calderon2020@gmail.com
- Phone: (714) 331-9825
- LinkedIn: www.linkedin.com/in/jesaiah-calderon-a045a029b
- Professional Summary: Motivated IT Support candidate with hands-on experience in
  Windows and Linux environments, user account management, troubleshooting, and
  basic networking. Currently preparing for CompTIA Security+ and building home lab
  experience in Active Directory, system administration, and security fundamentals.
  Strong customer service background and problem-solving skills from managing a
  small business.
- Certifications: CompTIA Security+, Google Cybersecurity Certificate
- Experience: Operator — Flowers by Jade (Small Business)
  - Provided daily technical troubleshooting for POS systems, computers, printers,
    and software
  - Managed online orders, website updates, and digital communication platforms
  - Delivered high-volume customer support while resolving issues efficiently
  - Maintained accurate records, scheduling, and workflow processes
  - Demonstrated strong communication, time management, and problem-solving skills

## Scope Decisions

- **Single page**, not multi-page. Original idea was separate pages per topic, but
  user decided everything fits on one scrollable page for now.
- Content is **not exactly resume-verbatim**: a Skills section is added, synthesized
  from the summary/experience/certifications (not present as its own section in the
  source doc).
- **Contact info is fully public**, including the phone number (explicitly confirmed
  after a privacy check-in during design).
- Each content block is a self-contained `<section id="...">` so that any one
  section could be lifted into its own page later without restructuring the rest
  of the site.

## Architecture

- Plain static HTML/CSS/JS. No framework, no build step, no dependencies.
- Three files: `index.html`, `style.css`, `script.js`.
- Sticky top nav bar with anchor links to each section (`#summary`, `#skills`,
  `#experience`, `#certifications`, `#contact`).
- Repo: `jesaiahcal.github.io` (GitHub "user site" repo — publishes automatically
  from `main` at the repo's root, no Pages configuration needed).

## Page Sections (in order)

1. **Header** — Name, title, location, sticky nav.
2. **Summary** — professional summary paragraph, lightly tightened for web reading.
3. **Skills** — grouped/derived list:
   - *Systems*: Windows & Linux environments, Active Directory, user account
     management
   - *Security*: CompTIA Security+ (in progress), Google Cybersecurity Certificate,
     security fundamentals home lab
   - *Support*: troubleshooting, networking basics, POS systems, customer service
4. **Experience** — Operator, Flowers by Jade (Small Business), with the five bullet
   points from the resume.
5. **Certifications** — CompTIA Security+, Google Cybersecurity Certificate.
6. **Contact** — email (mailto link), phone (tel link), LinkedIn link.

## Visual Design

- **Theme**: dark "cyber" aesthetic.
- **Palette**: near-black background (`#0a0e14`-ish), off-white body text, cyan/blue
  accent (`#33e0ff`-ish) for links, section headers, and highlights.
- **Type**: monospace font (e.g. JetBrains Mono / Fira Code) for headings and
  labels; clean sans-serif for body paragraphs so long text stays readable.
- **Layout**: centered single column, generous spacing, sticky top nav, subtle
  border/glow accents on section headers.
- **Background animation**: a low-opacity particle network on a full-viewport
  `<canvas>` behind the content — sparse dots drifting slowly, faint lines
  connecting nearby dots. Deliberately subtle: low opacity, slow movement, must not
  compete with text for attention.
  - Respects `prefers-reduced-motion`: animation is disabled (static or absent) for
    users with that OS setting enabled.
  - `pointer-events: none` on the canvas so it never blocks clicks/scroll/selection.

## Deployment Workflow

1. Site is built locally in `~/jesaiahcal.github.io/` and previewable by opening
   `index.html` directly in a browser (no local server required).
2. User creates an empty GitHub repo named exactly `jesaiahcal.github.io` via
   github.com (GitHub account actions are done by the user directly, not via
   automated browser control).
3. Locally: `git init`, `git add`, `git commit`, add the GitHub remote, `git push`
   to `main`.
4. No GitHub Pages configuration step needed — a `<username>.github.io` repo
   auto-publishes from `main` at the repo root.

## Verification

Since this is static HTML/CSS/JS with no backend or build step, verification is
manual:

- Open `index.html` locally and check layout/readability at desktop width.
- Resize to mobile width and confirm the layout stays usable.
- Click every link: `mailto:`, `tel:`, and the LinkedIn URL.
- Confirm the particle background stays subtle (low opacity, slow) and doesn't
  noticeably affect scroll performance.
- Confirm the animation disables under `prefers-reduced-motion`.
- After deploying, load `https://jesaiahcal.github.io` and re-check the above on
  the live URL.

## Out of Scope (for this iteration)

- Multi-page structure (deferred; sections are built to be splittable later if
  wanted).
- Downloadable resume PDF/DOCX link (considered, not selected).
- Custom domain.
- Automated tests / CI pipeline (not warranted for a static single-page site).

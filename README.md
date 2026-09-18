# Avokara website

Static HTML site for **www.avokaraai.com**. No build step, no framework, no
dependencies — every page is hand-editable HTML served straight from this
directory (GitHub Pages; `CNAME` + `.nojekyll`).

---

## Positioning

The site presents Avokara as a **technology engineering company**: it designs,
builds, integrates, deploys and maintains software and AI systems for
organisations with complex operational workflows — institutions, enterprises and
growing businesses alike.

Every page should be able to answer, for a reader who has never heard of us:

1. What does Avokara do?
2. What kind of problem can it solve?
3. Can it actually build and run serious software?
4. Can it handle integrations, data, security, APIs, dashboards, automation and
   long-term support?
5. Can it take a project from requirement through to maintenance?
6. Is the company structured and professional enough to be considered?

---

## Content rules

These are not style preferences. Breaking them creates a credibility problem
that is much more expensive than the sentence was worth.

- **Never publish a claim that cannot be substantiated.** No invented clients,
  contracts, revenue, headcount, project counts, user numbers, deployment
  statistics, awards or partnerships.
- **Never claim a certification, accreditation, registration or empanelment we
  do not hold** — including ISO/IEC 27001, SOC 2, CERT-In, STQC, GeM
  registration or any government security clearance. `/security/` and
  `/company-profile/` state plainly what we *do not* hold; keep that.
- **No case study without permission and real numbers.** Where an outcome cannot
  be measured or shared, say so rather than substituting a plausible figure.
- **Avoid** "revolutionary", "world-class", "best", "leading", "unmatched",
  "cutting-edge", "next-generation" unless there is evidence behind it.
- **Keep the "Honest limitations" section on every service page.** It is a trust
  signal, not a weakness — it tells a buyer where we would decline work.
- Placeholders that must be filled before publishing are marked in the HTML
  source with `PLACEHOLDER`, `TO ADD`, `ACTION REQUIRED` or
  `VERIFY BEFORE PUBLISH`. Search for those strings before a release.

---

## Outstanding items

| Where | What |
|---|---|
| `contact/index.html` | **Form backend is not configured.** Replace `REPLACE_WITH_YOUR_FORMSPREE_ID` in the form `action`. Until then, an inline script detects the placeholder and falls back to a pre-filled `mailto:` so the page still works. |
| `company-profile/index.html`, `about/index.html` | Commented-out rows for GSTIN, company PAN, Udyam/MSME registration and a business telephone number. Uncomment and fill **only** once you hold the document. |
| `capabilities/index.html`, `company-profile/index.html` | `VERIFY BEFORE PUBLISH` comment above each technology list. Delete anything Avokara cannot currently deliver; add what it can (Laravel/PHP, Vue, Flutter, Kotlin, MongoDB, a named cloud provider) once confirmed. |
| `case-studies/` | Only the internal build is published. Add client case studies as projects complete and clients agree — Challenge / Solution / Architecture / Technology / Outcome. |
| Mobile apps | `services/custom-software-development/` states explicitly that native iOS/Android is **outside** current delivery. Remove that limitation only when it stops being true. |

---

## Structure

```
/                                   Home — positioning, capability snapshot, services,
                                    solutions, delivery, security, project types,
                                    sectors, differentiators, evidence, FAQ
/services/                          Hub: 7 engineering services + 5 function solutions
  ai-agent-development/             AI agents & intelligent automation
  custom-software-development/      Applications, portals, dashboards, workflow systems
  digital-transformation/           Process digitisation, legacy modernisation
  api-system-integration/           REST APIs, middleware, webhooks, synchronisation
  data-analytics-dashboards/        Operational dashboards, MIS, automated reporting
  cloud-infrastructure-devops/      Deployment, database architecture, monitoring, backups
  support-maintenance/              Ongoing support, updates, performance, enhancement
  sales-lead-automation/            ┐
  customer-support-automation/      │ function-level automation pages (pre-existing,
  finance-operations-automation/    │ kept for the search traffic they carry)
  marketing-content-automation/     │
  workflow-automation-n8n/          ┘
/capabilities/                      Engineering disciplines + technologies per discipline
/solutions/                         7 problem-oriented solution areas (+ #anchors)
/how-we-work/                       8-stage delivery process and the output of each stage
/security/                          Security & reliability practices; what we do not claim
/company-profile/                   Printable capability profile (print → Save as PDF)
/industries/                        9 sectors; 4 have detail pages
/case-studies/                      Selected work + how to evaluate a young supplier
/pricing/                           Engagement models and indicative ranges
/about/  /faq/  /blog/              Company, FAQ, insight articles
/privacy-policy/  /terms/           Legal
/404.html                           Not-found page (served by GitHub Pages)
/assets/styles.css                  The entire design system — single stylesheet
```

## Design system

`assets/styles.css` is the only stylesheet. Navy `#101828` / red `#e5352e` /
white; Poppins for headings, Inter for body.

- **Contrast:** every text element on the site passes WCAG AA (verified across
  all pages). Two rules keep it that way:
  - `--red` (#e5352e) is only 4.29:1 on white. Use `--red-dark` for red *text*
    and button fills; keep `--red` for decorative accents (icon tints, logo dot).
  - `--muted` (#667085) is tuned for light backgrounds. On the navy footer use
    `#98a2b3` — `.site-footer .muted` already does this.
- **Two `:not(.btn)` selectors are load-bearing.** `.nav-list a:not(.btn)` and
  `.section-dark a:not(.btn)` exist because both rules out-specify `.btn-primary`
  and `.btn-light`. Drop the `:not(.btn)` and button labels render navy-on-red
  in the header and white-on-white in dark sections.
- **Grid tracks use `minmax(0,1fr)`, never `1fr`.** A wide child such as a table
  will otherwise stretch its track past the container and cause horizontal page
  scroll on mobile.
- **Icons are inline SVG** inside `<span class="icon" aria-hidden="true">`.
  Do not reintroduce emoji icons — they were the strongest "cheap agency" signal
  on the previous version of the site.
- Key components: `.snapshot` (capability strip), `.cap` / `.cap-grid`
  (capability blocks), `.phases` (delivery timeline), `.rail` (lifecycle),
  `.tag-grid` (project types), `.stack` (technology pills), `table.spec`
  (light key/value table), `.note` (callout), `.doc-card`, `.section-dark`.

## Editing a page

Header and footer are inlined on every page (no templating — it keeps the site
dependency-free and fast). A navigation or footer change therefore has to be
applied to every `*.html` file: edit one, then find-and-replace the block
between `<header class="site-header">` … `</header>` and
`<footer class="site-footer">` … `</footer>` across the tree.

## SEO and answer engines

Every page carries JSON-LD: `Organization` + a page node (`WebPage`, `AboutPage`,
`ContactPage`, `CollectionPage`) + `BreadcrumbList`, plus `Service`, `FAQPage`,
`OfferCatalog`, `ItemList`, `Person` or `Article` where relevant.

Rules that are checked and must hold:

- **One node per entity type per page.** Two `FAQPage` nodes on one page is a
  structured-data error — it happened once already when a page was typed
  `FAQPage` *and* rendered a Q&A block.
- **FAQ schema must match the visible questions exactly**, in the same order.
  If you add, remove or reword a `<details class="faq">` block, update the
  `FAQPage` node with it.
- **Title / meta description changes must be mirrored** in the page node's
  `name` / `description`, and in `og:` and `twitter:` tags.
- `<meta name="robots">` is `index, follow, max-image-preview:large,
  max-snippet:-1, max-video-preview:-1` on every page — `max-snippet:-1` lets
  answer engines quote a full passage. `404.html` is `noindex, follow`.
- **Answer-first paragraph.** Every page opens with a `.answer` block holding a
  self-contained, quotable definition. This is what AI answer engines extract,
  so it must read correctly with no surrounding context. Keep it on new pages.

Two files exist for AI crawlers:

- **`llms.txt`** — a curated map of the site for LLM retrieval, including an
  explicit *"Accuracy notes for summarisation"* section stating that Avokara
  holds no ISO 27001 / SOC 2 / empanelment, publishes no client or revenue
  figures, and does not build native mobile apps. **Update it when the site
  changes** — a stale `llms.txt` teaches answer engines the wrong thing.
- **`robots.txt`** — allows all crawlers, and names the AI agents (GPTBot,
  ClaudeBot, PerplexityBot, Google-Extended, Applebot-Extended, etc.)
  explicitly so the intent to be indexed and quoted is unambiguous.

`assets/og-image.png` (1200×630) is what appears in WhatsApp, LinkedIn and Slack
previews. It is generated from `assets/avokara-logo.png` recoloured white on the
brand navy. **If the positioning changes, regenerate it** — it previously still
read "AI Business Automation", contradicting the rest of the site.

## Local preview

```bash
python -m http.server 8099
```

Then open <http://localhost:8099>. There is nothing to compile.

After editing, check: one `<h1>` per page, `<title>` ≤ 70 characters, meta
description 70–165 characters, no horizontal scroll at 375px width, and add new
pages to `sitemap.xml`.

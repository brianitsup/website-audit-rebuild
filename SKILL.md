---
name: website-audit-rebuild
description: Audit an existing publicly accessible website and produce a complete redevelopment plan — page/content/feature inventory, sitemap, multi-area audit (UI, UX, mobile, accessibility, performance, SEO, security, branding, content, architecture, analytics), a client-facing audit report, a technical redevelopment specification with content migration plan, and a concise (≤3 page) redevelopment proposal with tasks, conservative timeline and budget, and recommended tech stack. Use this skill whenever the user asks to audit, review, analyze, assess, redesign, rebuild, modernize, migrate, or "look at" an existing website or URL; wants a website proposal, quote, or scope for improving a client's site; asks "what's wrong with this site"; or wants to document a site before redeveloping it. Trigger even if the user only pastes a URL and asks for feedback on the site.
---

# Website Audit & Rebuild

Turn a live website into two professional deliverables: (1) an **audit report** the website owner can read, and (2) a **technical redevelopment specification** a developer can build from — plus the supporting inventories and migration plan that make sure nothing important is lost in the rebuild.

## Operating principles

These govern everything below:

1. **Public content only.** Inspect only what an anonymous visitor can reach. Never bypass logins, paywalls, CAPTCHAs, or access controls. If the user supplies credentials AND states they own or are authorized to audit the site, authenticated areas may be reviewed manually with the user (do not automate credentialed crawling). Record the authorization claim in the report's assumptions.
2. **Respect the site.** Check `/robots.txt` first and honor Disallow rules and crawl-delay. Fetch pages sequentially with pauses (1–2s between requests; more if the server is slow — common for Pacific-hosted sites). Cap total fetches by site tier (see Sizing). Stop and tell the user if the site blocks you rather than working around it.
3. **Document, don't copy.** Record structure, content topics, functionality, and design patterns. Quote at most short snippets as evidence. Do not bulk-copy proprietary text, source code, or download protected assets. The content migration plan maps *where content lives and where it goes*, not a wholesale scrape.
4. **Confirmed vs. assumed — always labeled.** Everything you state is one of: **[Confirmed]** (directly observed on the public site), **[Inferred]** (reasonable deduction from evidence — say what the evidence is), or **[To confirm with owner]** (cannot be verified externally: hosting details, admin workflows, traffic data, business goals, backend integrations, content ownership). Carry these labels through every deliverable. A rebuild spec full of unlabeled guesses causes scope disputes later; the labels are what make the spec trustworthy.
5. **Evidence over adjectives.** "The homepage loads 4.2 MB of images and has no caching headers" beats "the site is slow." Every audit finding needs at least one concrete observation behind it.

## Workflow overview

```
0. Scope with user  →  1. Recon & sizing  →  2. Crawl & inventory
→  3. Functionality mapping  →  4. Multi-area audit  →  5. Findings & priorities
→  6. Deliverable A: Audit report  →  7. Deliverable B: Redevelopment spec
→  8. Content migration plan  →  9. Deliverable C: Proposal  →  10. Package & present
```

For a small site this can run end-to-end in one pass. For medium/large sites, checkpoint with the user after step 2 (inventory) and step 5 (findings) before writing the big documents.

## Step 0 — Scope with the user

Before fetching anything, establish (ask only for what's missing; don't interrogate):

- The URL, and whether the user owns the site / is authorized by the owner / is prospecting (public review only).
- Purpose: full rebuild plan, audit-only, or proposal/quote support? (Audit-only → skip deliverable B; proposal → both, with the spec framed as scope.)
- Any known context: CMS, hosting, known problems, business goals, budget/timeline constraints, preferred stack.
- For the proposal: the user's day rate or price bands, currency, and any recurring costs they pass through (hosting, licences). Without rates, the proposal will show effort-days with rate placeholders — never invented prices.
- Output format preference: Markdown files (default), Word documents (use the docx skill), or both.

If the user just says "audit example.com", proceed with sensible defaults (full audit + spec, Markdown) and note the defaults chosen.

## Step 1 — Recon & sizing

Fetch, in order:

1. `https://site/robots.txt` — note Disallow rules, crawl-delay, sitemap references.
2. `https://site/sitemap.xml` (and any sitemaps referenced in robots.txt) — this is the fastest way to size the site.
3. The homepage.

From these, classify the site tier and set the crawl budget:

| Tier | Indicators | Crawl budget | Analysis depth |
|---|---|---|---|
| **Small** | ≤ ~25 pages; brochure/informational | Fetch every page | Full per-page notes |
| **Medium** | ~25–150 pages; blog/news, multiple sections | All templates + all top-nav pages + representative sample per section (3–5 each) | Per-template depth, per-page for key pages |
| **Large** | 150+ pages; e-commerce, portals, directories | Every distinct *template* + section landing pages + samples; rely on sitemap for the URL inventory | Template-level; flag that page-level QA needs a scripted crawl during the rebuild project |

If there's no sitemap.xml, size from navigation breadth-first and say so — the URL inventory will be labeled [Inferred] complete rather than [Confirmed].

Also capture during recon: HTTPS status and certificate validity, redirect behavior (http→https, www/non-www), response headers (server, caching, security headers), and any obvious platform fingerprints (e.g., `/wp-content/` → WordPress, `cdn.shopify.com` → Shopify, `__NEXT_DATA__` → Next.js).

## Step 2 — Crawl & inventory

Fetch pages per the budget, breadth-first from navigation + sitemap. For each page record into a working inventory (a table or structured notes you maintain as you go — don't rely on memory across dozens of fetches; write it down incrementally):

- URL, title tag, meta description, H1
- Page type/template (home, service page, blog post, contact, listing…)
- Content summary (2–3 lines: what the page says, roughly how much content, freshness signals like dates)
- Media: images (count, whether alt text appears present), embedded video, downloads (PDFs etc. — list them, don't download unless needed as evidence)
- Forms and interactive elements
- Internal links out; note any that 404 or redirect (broken-link findings come from here)
- External links and embedded third parties (analytics, chat widgets, maps, social embeds, fonts, CDNs)
- Anything odd: placeholder text, lorem ipsum, mixed languages, staging URLs, mixed-content warnings

This inventory is the raw material for four final artifacts: the **page inventory**, **sitemap** (current-state tree), **content inventory**, and the broken-link/issue list. Build them from the same pass — don't crawl twice.

## Step 3 — Functionality mapping

From the crawl evidence, enumerate every feature the site offers, each labeled Confirmed/Inferred/To-confirm:

Contact & lead forms · site search · authentication/login/user accounts · dashboards or member areas (note existence from login links even though you can't enter) · booking/reservation systems · e-commerce (catalog, cart, checkout, payment providers visible) · newsletters/subscriptions · multilingual content and language switching · maps/location features · file downloads/resources · comments/community · chat/support widgets · APIs or embedded apps · CMS indicators · analytics & tracking (GA/GTM/Meta pixel etc., visible in page source) · cookie/consent tooling.

For each: what it does, where it appears, what powers it (if fingerprinted), and whether it must be **preserved, improved, or retired** in the rebuild (mark "owner decision" where it's not obvious). This preserve/improve/retire mapping is what fulfills the "nothing important gets lost" guarantee — it feeds directly into the migration plan.

## Step 4 — Multi-area audit

Audit across all eleven areas using `references/audit-checklists.md` — read it now; it contains the per-area checklists, what evidence to gather for each, and severity guidance. The areas:

1. UI & visual design · 2. UX & navigation · 3. Mobile responsiveness · 4. Accessibility · 5. Performance · 6. SEO · 7. Security & privacy · 8. Branding consistency · 9. Content quality & structure · 10. Technical architecture & maintainability · 11. Analytics & third-party integrations

Honest scoping note to apply throughout: some checks can't be fully performed from static fetches (real device rendering, Core Web Vitals field data, JS-executed behavior). Do what the evidence allows, use public tools where available (e.g., suggest the owner's PageSpeed Insights results as follow-up), and label the rest [To confirm]. Never fabricate scores or metrics.

## Step 5 — Findings & priorities

Consolidate every issue into a findings register: ID, area, description, evidence (URL + observation), severity (Critical / High / Medium / Low), effort (S/M/L), and recommendation. Also capture **strengths** — things worth keeping (good content, strong brand assets, working features). Owners hear "everything is broken" as a sales pitch; a credible audit names what already works.

Priority = severity × reach ÷ effort, tempered by judgment: a Critical security issue on one page outranks a Medium UX issue everywhere. Group into: **Fix now (pre-rebuild)** · **Fix in rebuild** · **Nice-to-have / phase 2**.

Checkpoint with the user here on medium/large sites: share the findings summary and confirm direction before writing the two big documents.

## Step 6 — Deliverable A: Audit report (for the website owner)

Write for a non-technical business owner: plain language, jargon explained, evidence shown, every recommendation tied to a business outcome (more enquiries, fewer support calls, better search visibility — not "better Lighthouse score"). Use the structure in `references/report-template.md`. Screenshots: if the environment can capture them, include key evidence images; otherwise reference URLs precisely and quote the observable evidence.

## Step 7 — Deliverable B: Technical redevelopment specification

Write for the developer/team who will build it. Use the structure in `references/spec-template.md`. Key requirements for this document:

- **Stack recommendation must be justified**, not defaulted. Weigh: site complexity, content-editing needs (who updates content and how technical are they), budget, hosting realities, and maintenance capacity. Present the recommended stack with rationale and one alternative with trade-offs. If the user has stated preferred stacks, evaluate those first — but say honestly if the site's needs point elsewhere (e.g., a 10-page brochure site for a low-budget client with non-technical editors may genuinely be a WordPress or static-site job, not a custom SaaS stack).
- **Page-by-page requirements** derive from the inventory: for each page/template — purpose, content source (migrated / rewritten / new), functional elements, and acceptance criteria.
- **Data models** only where the site actually has structured data (products, bookings, listings, users). Don't invent schemas for a brochure site.
- Every requirement labeled Confirmed/Inferred/To-confirm, and the open-questions list at the end is the owner-meeting agenda.

## Step 8 — Content migration plan

A table mapping every current page/content asset → destination in the new sitemap → action (migrate as-is / rewrite / merge / retire) → owner of that action → redirect needed (old URL → new URL). Include: media assets, downloads, form-submission continuity, and a 301-redirect map for every retired or moved URL (this protects SEO — say so in the plan). Flag content whose copyright/ownership is unclear as [To confirm].

## Step 9 — Deliverable C: Proposal (max 3 A4 pages)

A concise commercial document the owner can say yes to: background & objectives, scoped tasks by phase (with explicit exclusions), recommended stack in owner language, conservative timeline, conservative budget with visible contingency, assumptions, next steps. Use `references/proposal-template.md` — it contains the budget and timeline rules, which are strict: never invent market rates (use user-supplied rates or effort-day placeholders), always show ranges with contingency, always separate one-off build cost from recurring annual cost, and pad timelines for owner-side content delays. The proposal must reconcile with the report's phases and the spec's stack — cross-check before finalizing. Hard limit three A4 pages; move depth to the other deliverables, not into smaller fonts.

## Step 10 — Package & present

Assemble final outputs. Default file set (Markdown in an `audit-<sitename>/` folder; convert to docx via the docx skill if requested):

```
audit-<sitename>/
├── 01-website-inventory.md      (pages, URLs, media, downloads, links)
├── 02-sitemap-current.md        (current-state tree) + proposed sitemap lives in the spec
├── 03-feature-inventory.md      (functionality map w/ preserve-improve-retire)
├── 04-content-inventory.md
├── 05-audit-findings.md         (full findings register + strengths)
├── 06-audit-report.md           (Deliverable A — owner-facing)
├── 07-redevelopment-spec.md     (Deliverable B — developer-facing)
├── 08-content-migration-plan.md
├── 09-risks-assumptions-questions.md
└── 10-proposal.md               (Deliverable C — owner-facing, ≤3 A4 pages)
```

For **small sites**, it's fine to merge 01–04 into a single inventory document and 08–09 into the spec — adjust to the site, not the template. Present the files to the user with a short summary: top 3 findings, recommended direction, and what needs the owner's confirmation.

## Failure and edge handling

- **Site unreachable / blocks fetching**: report what happened; offer to work from screenshots or an export the user provides. Do not circumvent.
- **robots.txt disallows everything**: tell the user; audit only the pages they explicitly provide or the homepage if permitted, and note the limitation prominently.
- **JS-only rendering (SPA with no SSR)**: static fetches may return near-empty HTML. Note this as itself a Critical SEO finding, work from what's fetchable + user-provided screenshots, and label coverage limits.
- **Huge sites**: don't attempt exhaustive crawling; template-level audit + sitemap-based inventory, and recommend a scripted crawl as a rebuild-project task.
- **Sensitive content encountered** (exposed personal data, security vulnerabilities): document the finding for the owner as Critical, do not include the exposed data itself in deliverables, and advise responsible handling.

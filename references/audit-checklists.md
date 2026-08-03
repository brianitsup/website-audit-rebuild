# Audit Checklists — 11 Areas

For each area: what to check, what evidence looks like from static fetches, and how to judge severity. Apply only the checks relevant to the site — skip e-commerce checks on a brochure site. Every finding = observation + URL + severity + recommendation.

Severity guide (used across all areas):
- **Critical** — actively losing the owner money, users, or safety: broken checkout/contact paths, security exposure, site unusable on mobile, legally required items missing.
- **High** — materially hurts outcomes: major SEO defects, slow key pages, inaccessible core journeys, broken primary navigation.
- **Medium** — friction and quality problems: inconsistent design, thin content, minor a11y issues, outdated info.
- **Low** — polish: minor visual inconsistencies, nice-to-have optimizations.

---

## 1. UI & visual design

Check: visual hierarchy on key pages (is the primary action obvious?); typography (how many typefaces/sizes; readability; line lengths); color usage and contrast (also an a11y check); spacing consistency; image quality (blurry, stretched, watermarked stock, inconsistent aspect ratios); dated design signals (skeuomorphism, tiny body text, carousels-as-homepage, table layouts); consistency of buttons/links/cards across pages.

Evidence from fetches: inline styles vs. stylesheet count, CSS frameworks fingerprinted, image dimensions vs. display size, heading font stacks in CSS. Judgment calls about "dated" should cite specifics ("navigation uses image-based buttons, a pre-2010 pattern") not taste alone.

## 2. UX & navigation

Check: primary nav clarity (≤7 top items is a norm, not a law); can a first-time visitor tell within seconds what the org does and what to do next; menu depth and orphan pages (in sitemap but linked from nowhere); breadcrumbs on deep sites; footer as a usable secondary nav; contact info findability (phone/email/address within one click — vital for local businesses); CTA presence and consistency; 404 page (fetch a garbage URL — does it help or dead-end?); search availability on content-heavy sites; form friction (field count vs. purpose; a contact form demanding 10 fields is a finding).

## 3. Mobile responsiveness

Static-fetch checks: viewport meta tag present and correct; responsive CSS (media queries present? fixed-width layouts?); separate m. subdomain (a legacy pattern worth flagging); image srcset/sizes usage; tap-target hints (nav structure that implies hover-dependence, e.g., CSS :hover dropdown menus with no click handling — unusable on touch); font sizes in CSS below ~14px for body text; horizontal-scroll risks (fixed pixel widths > 400px on containers).

Label real-device rendering as [To confirm] — recommend the owner or developer verify on actual devices. If no viewport tag and no media queries: the site is effectively desktop-only → Critical (mobile is the majority of traffic for most Pacific audiences).

## 4. Accessibility

Static checks (WCAG 2.1 AA orientation): image alt attributes (present? meaningful, or filenames?); heading hierarchy (one H1, no skipped levels); form inputs with associated labels; link text ("click here" vs. descriptive); color-contrast estimates from CSS color pairs; language attribute on <html>; skip-to-content link; ARIA misuse (aria attributes on wrong elements is worse than none); keyboard traps implied by JS-only click handlers on non-interactive elements; video captions availability; PDFs as sole source of key info (flag — often inaccessible).

Be honest about scope: a static audit finds structural issues; full a11y compliance needs manual keyboard/screen-reader testing → list as rebuild acceptance criterion, not something this audit certifies.

## 5. Performance

Static checks: total page weight of key pages (sum fetched asset sizes where determinable); image formats (large PNG/JPEG where WebP/AVIF would serve; uncompressed hero images are the #1 real-world issue); number of render-blocking scripts/styles in <head>; caching headers (Cache-Control, ETag); compression (Content-Encoding: gzip/br); redundant libraries (three jQuery versions happens more than you'd think); font loading strategy; CDN usage; server response time (time-to-first-byte from your fetches, noting your vantage point differs from users').

Frame findings for the local context where relevant: heavy pages punish users on slow/expensive island connections — this is a business argument, not just a technical one. Recommend PageSpeed Insights / WebPageTest runs as confirmation; never invent Core Web Vitals numbers.

## 6. SEO

Check: title tags (present, unique per page, sensible length ~50–60 chars); meta descriptions (present, unique, compelling); one H1 per page matching intent; URL structure (readable vs. ?id=123); canonical tags; sitemap.xml exists and matches reality; robots.txt not accidentally blocking the site; structured data (LocalBusiness, Product, Article JSON-LD — especially valuable for local businesses); Open Graph/social tags; image alt text (dual a11y/SEO); internal linking (orphans, reasonable anchor text); duplicate content (same content at multiple URLs, http+https both live, www/non-www unredirected); obvious thin/doorway pages; hreflang if multilingual; Google Business Profile linkage hints.

For redevelopment: the 301 redirect map (migration plan) is the single most important SEO deliverable — losing existing rankings in a rebuild is the classic self-inflicted wound. Say this explicitly in reports.

## 7. Security & privacy

Public-surface checks only — this is not a penetration test and must not be presented as one. Check: HTTPS enforced (http→https redirect; no mixed content); certificate validity; security headers (CSP, X-Frame-Options/frame-ancestors, HSTS, X-Content-Type-Options, Referrer-Policy); visible software versions (WordPress version in meta generator, plugin readme files, outdated jQuery — version disclosure + known-EOL software = finding); exposed files (/wp-config.php.bak style leftovers, .git/ directory, listing-enabled directories — check a few common paths, do not brute-force); forms posting over http; login pages without rate-limit hints (note, To-confirm); privacy policy existence and cookie consent where third-party tracking exists; email addresses exposed as plaintext (spam harvest risk — minor); payment pages: are they on the site or delegated to a provider (delegation is usually good news).

If you find an actual exposure (dumped database, credentials, personal data): Critical finding, describe the class of exposure and location for the owner, exclude the data itself from all documents, and advise immediate remediation.

## 8. Branding consistency

Check: logo usage (same version everywhere? stretched? low-res?); color palette drift across pages/sections; typography drift; tone-of-voice consistency in copy; imagery style coherence; favicon and social-share images present; brand name spelled/styled consistently; email addresses and phone formats consistent; old brand remnants after a rename (common); consistency between site and any visible social profiles linked from it.

Output feeds the spec: a starter design-token list (colors, type scale, spacing) the rebuild should formalize — extracted from what's worth keeping.

## 9. Content quality & structure

Check: freshness (dated content — "News" last updated 2021 is worse than no news section); accuracy signals (prices, staff lists, opening hours — flag anything the owner must verify); completeness (empty sections, "coming soon" pages); readability (wall-of-text pages, missing subheadings); duplication across pages; spelling/grammar patterns (note the pattern, don't list every typo); placeholder/lorem-ipsum survivals; key business content present (about, services, contact, and sector-specifics like menus/rates/schedules); content-to-page fit (does each page have a job?); PDFs carrying content that should be HTML; multilingual completeness (partial translations are a common finding).

## 10. Technical architecture & maintainability

Check: platform/CMS identification and version; hosting fingerprints (headers, IP/ASN, CDN); theme/plugin sprawl signals on WordPress; hand-coded vs. generated markup quality; inline styles/scripts everywhere (maintainability smell); asset organization; dead code in page source; dependency ages; whether content editors could plausibly update the site (CMS present?) or every change needs a developer (business risk for the owner); form handling (mailto: links are a finding — unreliable); backup/staging indicators (usually To-confirm); domain/DNS observations (registrar-parked subdomains, SPF/DMARC presence via DNS if checkable — affects their email deliverability and is worth a note).

## 11. Analytics & third-party integrations

Enumerate every third-party request the pages make: analytics (GA4/Universal-legacy — flag dead UA properties, GTM, Matomo, Meta pixel, LinkedIn tag), chat widgets, maps, fonts, CDNs, social embeds, review widgets, booking/payment providers. For each: purpose, whether it still works (legacy UA = collecting nothing since 2023), privacy implications (consent required?), performance cost, and rebuild disposition (keep/replace/drop). Absent analytics on a business site is itself a High finding — the owner is flying blind and the rebuild's success can't be measured without a baseline.

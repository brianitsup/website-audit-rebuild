# Redevelopment Specification Template (Deliverable B — for the build team)

Audience: the developer(s) who will build the new site — possibly the auditor themselves, possibly a contractor months later with no other context. Write so it stands alone. Every requirement carries a [Confirmed]/[Inferred]/[To confirm] label; unresolved [To confirm] items also appear in §18 as the open-questions list.

Structure:

```markdown
# Website Redevelopment Specification — <Site name>
Version · Date · Author · Status (Draft / Confirmed with owner)

## 1. Project goals
3–6 measurable goals tied to the audit findings ("recover mobile traffic",
"cut page weight below X", "enable owner self-service content editing").
Each goal traces to audit finding IDs.

## 2. Target audiences
Primary/secondary audiences with the context that shapes decisions:
devices, connection quality, language(s), digital literacy. [Inferred from
site content unless the owner has confirmed audience data.]

## 3. Proposed sitemap
New-state tree. Beside each node: source (existing page ID from inventory /
merged from pages X+Y / new). Orphaned current pages must appear in the
migration plan as retire-with-redirect — the two documents must reconcile.

## 4. Page-by-page requirements
Per page or template:
  - Purpose and primary user action
  - Content source: migrate / rewrite / new (who writes it)
  - Functional elements (forms, embeds, dynamic data)
  - Acceptance criteria (concrete, testable: "form submission delivers
    email to X and shows confirmation", "page renders correctly at 360px")

## 5. Functional requirements
Every feature from the feature inventory marked preserve/improve, plus new
features. For each: description, user roles involved, inputs/outputs,
edge cases, and the audit-inventory ID it traces to. Features marked
"retire" are listed briefly with the retirement rationale.

## 6. UI & UX requirements
Navigation model, layout principles, key user journeys (steps each journey
must support), form UX standards, error/empty/loading states, content
hierarchy rules. Reference wireframes if produced (optional at this stage).

## 7. Branding & design system
What carries over (from the branding audit): logo files needed, color
tokens, type scale, spacing scale, component inventory (buttons, cards,
forms…). What gets refreshed and who decides. Deliverable: a small token
set the build implements, not a full brand manual.

## 8. Accessibility requirements
Target: WCAG 2.1 AA (adjust only with owner sign-off). Concrete build
requirements: semantic HTML, keyboard operability, focus states, contrast
tokens ≥ 4.5:1 body text, alt-text authoring responsibility, testing gates
(automated checks in CI + manual keyboard/screen-reader pass before launch).

## 9. Security requirements
HTTPS + HSTS; security headers baseline (CSP, frame-ancestors, referrer-
policy, content-type-options); auth requirements if user accounts exist
(password policy, rate limiting, session handling); form spam protection;
dependency update policy; backup and restore requirements; secrets handling;
privacy: consent management, privacy policy, data retention. Findings from
the audit's §7 each map to a requirement here.

## 10. SEO requirements
301 redirect map implementation (reference migration plan — launch gate);
per-page titles/descriptions from content plan; structured data to
implement; sitemap.xml + robots.txt; canonical strategy; performance
budgets as ranking factor; analytics goal tracking from day one.

## 11. Performance requirements
Concrete budgets appropriate to audience connectivity, e.g.: key pages
≤ X MB transfer, images in modern formats + responsive sizes, TTFB target,
caching and CDN strategy, third-party script budget. State budgets as
launch acceptance criteria.

## 12. Integration requirements
Each third party kept or added: service, purpose, data exchanged, auth
method, failure behavior, cost note [To confirm], and owner-account
access needed.

## 13. Recommended technology stack
The recommendation WITH rationale against: complexity of features, who
edits content (and their technical comfort), budget and hosting realities,
maintenance capacity, and longevity. Include one credible alternative and
the trade-off. If the implementer has stated house stacks, evaluate fit
honestly — recommend against a house stack when the site's needs don't
justify it, and say why.

## 14. Data models
Only if the site has structured data (products, bookings, users, listings,
multi-author content). Entities, key fields, relationships — schema-sketch
level, not final DDL. For brochure sites: state "no custom data model
required" and describe the CMS content types instead.

## 15. User roles & permissions
Roles (visitor, editor, admin, customer…), what each can do, and how
accounts are provisioned. Even simple sites need "who can edit content".

## 16. Content migration plan
Reference the standalone migration document; summarize counts (pages
migrated / rewritten / merged / retired) and the redirect-map obligation.

## 17. Testing & acceptance
Test types (functional, responsive matrix, accessibility, performance
budgets, forms end-to-end, redirect map verification, SEO checklist) and
the launch checklist. Acceptance = all page-level criteria (§4) plus these
gates.

## 18. Deployment & maintenance
Hosting recommendation with rationale; environments (at minimum staging +
production); deployment method; backup schedule; update/patching plan;
monitoring (uptime + analytics); content-editing handover and training;
documentation to deliver; ongoing-cost transparency [To confirm amounts].

## 19. Risks, assumptions, and open questions
Risk register (risk · likelihood · impact · mitigation); all standing
assumptions; and the consolidated [To confirm] list — this is the owner
meeting agenda and the sign-off checklist before build starts.
```

Guidance:
- Phases: mirror the phases proposed in the owner report; the spec details Phase 1 fully and later phases at outline level. Don't spec Phase 3 features in acceptance-criteria detail — that's wasted work that will change.
- Traceability is the quality bar: audit finding → requirement → acceptance criterion. A requirement that traces to nothing should justify its existence or be cut.
- Keep the spec modular: mark clearly what is MVP/Phase-1 versus later, so the build can start small without re-architecture later (e.g., choose a CMS/data structure in Phase 1 that Phase 2 features can extend).

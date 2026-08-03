# website-audit-rebuild

A Claude skill that audits an existing publicly accessible website and produces a complete redevelopment package:

- Website, feature, and content inventories + current-state sitemap
- 11-area audit (UI, UX, mobile, accessibility, performance, SEO, security, branding, content, architecture, analytics)
- Owner-facing audit report with prioritised findings and phases
- Developer-facing redevelopment specification with content migration plan and 301 redirect map
- Concise (≤3 A4 pages) redevelopment proposal with conservative timeline and budget

## Structure

```
SKILL.md                          # Workflow: scope → crawl → audit → deliverables
references/
├── audit-checklists.md           # Per-area audit checklists + severity guidance
├── report-template.md            # Owner-facing audit report structure
├── spec-template.md              # 19-section developer specification
└── proposal-template.md          # ≤3-page proposal with budget/timeline rules
```

## Principles

Public content only · respects robots.txt and rate limits · documents rather than copies · every claim labeled Confirmed / Inferred / To-confirm · never invents prices or performance scores.

## Install

Package with the skill-creator's `package_skill.py` (or zip the folder as `.skill`) and save it to your Claude profile, or use it directly in Claude Code.

---
Maintained by Brian Mangi — ITSUP Ltd, Honiara, Solomon Islands.

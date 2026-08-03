# Proposal Template (Deliverable C — for the website owner, max 3 A4 pages)

Purpose: a concise commercial document the owner can approve — the bridge between the audit ("here's what's wrong") and the spec ("here's exactly what we'll build"). Hard limit: **three A4 pages** (~1,400–1,600 words plus one or two small tables). If it's running long, cut detail, not sections — depth lives in the audit report and spec, which this document references.

## Budget rules — read before writing numbers

Money is the highest-risk content in this document. Follow these rules:

1. **Never invent market rates.** Pricing comes from the implementer, not the skill. At scoping (Step 0) ask for: day/hour rate or fixed-price bands, currency (default SBD for Solomon Islands clients unless told otherwise), and any known recurring costs they pass through (hosting, domains, licences).
2. **If rates were provided**: estimate effort per phase in days, multiply, then apply conservatism — round effort **up**, add a visible contingency line (25–40% for rebuilds; websites always surface surprises), and present a **range**, not a single number ("SBD X–Y"). The low end of the range should still be achievable on a bad week.
3. **If no rates were provided**: do NOT guess currency amounts. Present effort ranges in days per phase, state "priced at [your standard rate] — to be inserted", and tell the user the proposal needs their rates before it goes to the client. This is a deliberate gap, not a failure.
4. **Separate one-off from recurring.** Owners get burned by surprise annual costs. Always show build cost and yearly running cost (hosting, domain, licences, maintenance retainer if offered) as distinct figures, each marked estimate/actual.
5. Label every figure as an **estimate subject to confirmation of the open questions** (reference the To-confirm list). The proposal is not a fixed quote unless the user explicitly says to write it as one.

## Timeline rules

Conservative here too: estimate elapsed weeks, not just effort days — content gathering from the owner is the usual bottleneck, so build owner-dependency time into the timeline and say so ("Phase 1 assumes content and photos are supplied by week 2; delays here move the launch date"). Round up. A proposal that says 6 weeks and delivers in 5 builds trust; the reverse destroys it.

## Structure

```markdown
# Website Redevelopment Proposal — <Site name>
Prepared for · Prepared by · Date · Valid until (30 days default)

## 1. Background & objectives                                  (~⅓ page)
Two short paragraphs: what the audit found (reference the report),
and the 3–4 business objectives the rebuild achieves. No jargon.

## 2. Scope of work                                            (~¾ page)
The redevelopment tasks, grouped by phase, as a compact list or table:
  Phase 0 — Urgent fixes to current site (if any)
  Phase 1 — Core rebuild: design, build, content migration, testing, launch
  Phase 2 — Enhancements (outline only, separately quotable)
Each task: one line. Explicitly list what is OUT of scope (content
writing? photography? logo design? — the classic disputes) and what
the owner must provide.

## 3. Recommended technology & approach                        (~⅓ page)
The stack recommendation in owner language: what it is, why it fits
THEIR site (editing ease, running cost, reliability on local
connectivity), and the practical benefit ("you'll update prices
yourself without calling a developer"). One short paragraph + 3–4
bullet benefits. Technical detail lives in the spec.

## 4. Timeline                                                 (~⅓ page)
Table: phase · duration (weeks, conservative) · key milestone ·
what we need from you. Note the content-dependency caveat.

## 5. Investment                                               (~⅓ page)
Table: phase · effort (days) · cost range (or rate placeholder).
Contingency line shown, not hidden. Separate table/lines for annual
recurring costs. Payment terms if the user has standard ones
(e.g., deposit / milestone / completion) — otherwise "to be agreed".

## 6. Assumptions & exclusions                                 (~¼ page)
The 5–8 assumptions the price depends on, drawn from the To-confirm
list. If these change, scope and price change — say exactly that.

## 7. Next steps                                               (2–3 lines)
Confirm open questions → sign-off → start date. Acceptance line
(signature/date) if the user wants it contract-style.
```

## Writing guidance

- Tone: confident, plain, specific. This is a selling document but honesty is the selling point — the conservative numbers and visible contingency ARE the differentiator against lowball competitors who blow their budgets.
- Reconcile with the other deliverables: phases must match the audit report's phases; the stack must match the spec's recommendation; the assumptions must be a subset of the To-confirm list. Contradictions between documents are credibility killers.
- If output is docx (via the docx skill), verify the 3-page limit against the rendered document, not the markdown length; tighten if it spills.

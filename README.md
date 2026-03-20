# GRC Portal — UX Design Exercise

**Role:** UI/UX Engineer / Product Designer (ServiceNow + Enterprise Portal Experience)
**Time spent:** ~2.5 hours



---

## What I built

A compact UX package for a portal that surfaces security, compliance, and operational reporting data — designed for two distinct user types consuming the same underlying ServiceNow GRC data.

---

## Figma Links

Steps Documentation: [Figjam](https://www.figma.com/board/I7CSWcBlAQxEyte7hNOj3T/loop-steps?node-id=0-1&t=8OSBYkVY32BkHUKb-1)

User flow, Wireframe, Components, Handoffs: [Figma](https://www.figma.com/design/y7ZVDd7bjDISh7auOnZ6Zg/loop-task?node-id=6-90&t=FJ5W7cQKQAIsVPlb-1)

---

## Process

**1. Competitive analysis**
Audited ServiceNow GRC, Vanta, Drata, and Secureframe. Key finding: most tools conflate three distinct surfaces — status awareness, triage action, and stakeholder participation — into one undifferentiated dashboard. The recurring UX failure is no clear entry point signal and no prioritization hierarchy.

**2. User selection**
Two users, deliberately constrained:
- **Security/Compliance Analyst** — triage and action. Lives in the detail.
- **Ops/IT Manager** — oversight and escalation. Needs rollup health at a glance.

Two users is enough to justify the core IA split without over-expanding scope.

**3. Information architecture**
- Primary: Dashboard / Health Overview
- Secondary: Domain drilldowns (Security / Compliance / Operations)
- Tertiary: Record detail (individual finding or policy)

**4. User flow**
Single portal, role-based entry. Analyst lands in the Work Queue. Manager lands in the Health Overview. Both converge at Domain Drilldown and share the same Record Detail and action model.

**5. Wireframes**
Pair-designed with Claude AI as a structural starting point. Validated component decisions against competitive audit findings. Used Google Stitch to produce a draft with all research artifacts fed in. Four screens: Dashboard, Compliance Domain View, Record Detail, and Empty/Error State.

**6. Component design**
Extracted repeating patterns into a component set: Status Badge, Health Tile, Finding Row, Linked Evidence accordion, and Filter Bar. Each annotated with states, color logic, and interaction behavior.

**7. Engineering handoff**
One-page handoff covering ServiceNow data model mapping, static vs. dynamic fetch strategy, skeleton loading behavior, and accessibility requirements.

---

## Assumptions

- Portal is read-heavy with targeted write actions. It is not a workflow builder.
- ServiceNow is the system of record. This portal is a consumer of its APIs, not a replacement.
- Authentication and role assignment are handled upstream — the portal receives a role on session init and routes accordingly.
- Posture score is a computed rollup from ServiceNow. The portal does not recalculate it client-side.

---

## Tradeoffs

- Chose hub-and-spoke navigation over tabs — domain boundaries are meaningful enough to warrant distinct surfaces, and the Manager/Analyst split needs a clear home screen per role.
- Skipped notification center, vendor/third-party access, and multi-framework reporting — flagged as sprint 2.
- Wireframes are intentionally lo-fi. Fidelity would obscure structural decisions, which are what this exercise is testing.

---

## What I'd do next

Usability test the role-based entry split — specifically whether Managers actually want a separate landing or prefer a configurable dashboard. Explore the escalation flow in more depth: what happens after you escalate, who gets notified, and how that maps to ServiceNow Task creation.

---

# AI Usage Note

**Tools used:** Claude (Anthropic), Google Stitch

## Where AI helped

- Scaffolding the IA structure and component vocabulary quickly, so time could be spent on decisions rather than blank-page setup
- Generating annotation content and engineering handoff copy as a first draft
- Producing the interactive wireframe HTML as a structural base to react against
- Competitive audit synthesis across 4 GRC platforms

## What it got wrong or I overrode

- Claude's default layout skewed card-heavy. Replaced with table-first views for the compliance domain — analysts need density, not cards.
- Initial sidebar nav suggestion was too heavyweight for a reporting portal. Simplified to a minimal left rail.
- AI defaulted to showing all four badge states as equal weight. Corrected hierarchy so Fail carries the highest visual weight and Exception is deliberately quieter.
- Google Stitch produced a reasonable draft but required manual correction of information hierarchy — it flattened primary and secondary content into the same visual weight.

## Where original reasoning mattered more

- The role-split entry point decision. AI suggested separate products; I pushed for a single portal with routing — a meaningful product thinking call that required understanding the enterprise context.
- The decision to use accordions for progressive disclosure on the Record Detail. AI suggested tabbed panels; accordions better preserve context and reduce cognitive overhead for analysts working through a checklist.
- Scoping. AI consistently suggested more screens. The constraint to four was a deliberate judgment call.

# Keystone AI — KDAT Milestone Ledger

This is the public milestone ledger for Keystone AI's KDAT (Keystone
Deliverable Acceptance Test) program. It records what has been built,
what has been proven, and what the evidence basis is for each claim.

It is not a product brochure. It is not a marketing site. It is an evidence
ledger designed to let technical readers evaluate claims against stated proof.

---

## What is KDAT?

KDAT milestones are numbered capability deliverables in the Keystone AI
development program. Each milestone defines a discrete technical capability
that can be demonstrated and verified. Milestones are numbered sequentially
(KDAT-001A, KDAT-002, KDAT-003, …) and may have sub-milestones (011A, 011B,
011C).

The KDAT program covers a governed AI retrieval and decision-support system
for first-responder and operational contexts.

---

## How to read this repo

Each milestone has a page in [milestones/](milestones/). Every page has:

- **Status** — current lifecycle state
- **Evidence class** — how strong the backing evidence is
- **What this proves** — exactly what was demonstrated
- **What this does NOT prove** — explicit scope limits
- **Public-safe claims** — language safe to use externally
- **Verification** — tests and smoke locks cited

Before citing any milestone, read the full page. Pay particular attention to
the evidence class and the "does NOT prove" section.

---

## Evidence classes

Evidence class is the most important signal on any milestone page.

| Class | Meaning |
|-------|---------|
| **Proven on current branch** | Delivery commits exist on the tracked branch, test scripts pass, smoke locks in place |
| **Historical baseline** | Pre-dates the current branch; referenced as prior work foundation |
| **Curated summary** | Derived from a human summary; no branch commits in this log to directly verify |
| **Doc-only reference** | Appears in documentation but no dedicated technical delivery commit |
| **Underdocumented** | Some evidence exists but insufficient to fully characterize the milestone |
| **Unknown** | Insufficient evidence; status not determinable from available data |

Curated summary is NOT the same as proof. Doc-only is NOT the same as delivered
technical capability.

See [docs/evidence-classes.md](docs/evidence-classes.md) for full definitions.

---

## No overclaiming

This repository will not claim:

- Enterprise readiness unless explicitly proven
- High availability or disaster recovery unless a milestone proves it
- Multi-node or distributed deployment unless a milestone proves it
- OIDC, ABAC, or production-hardened identity unless a milestone proves it
- Any capability "in production" unless deployment evidence exists

When evidence quality is weaker, the page says so.

---

## Current snapshot

Generated from branch `lrfd-backend-bootstrap` (2026-03-14).

| Category | Count |
|----------|-------|
| Proven on current branch | 12 |
| Historical baseline | 2 |
| Curated summary | 8 |
| Doc-only reference | 1 |

Branch HEAD SHAs at generation time:
- keystone-gov: `93aa470`
- keystone-console: `8f7abd5`
- keystone-deploy: `3dbaaa0`

---

## Navigation

- [All milestones](milestones/README.md)
- [Claims matrix](docs/claims-matrix.md)
- [Roadmap](docs/roadmap.md)
- [By status](index/by-status.md)
- [By evidence class](index/by-evidence-class.md)
- [By capability](index/by-capability.md)
- [Timeline](index/timeline.md)
- [Publication policy](docs/publication-policy.md)
- [Evidence class definitions](docs/evidence-classes.md)

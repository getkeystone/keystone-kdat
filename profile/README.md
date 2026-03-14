# Keystone AI

On-prem AI knowledge infrastructure for organizations that cannot rely on cloud AI.

Built for regulated and compliance-constrained environments where data sovereignty, access control, evidence-backed answers, and auditability matter. Core operation runs entirely on customer infrastructure with no external API dependency.

## What this GitHub organization contains

This organization is split into two layers:

- **Product and implementation repos** for the governed retrieval system, console, governance, and deployment
- **Public milestone ledger** that shows what is proven today, what is historical baseline, and what is not ready to claim publicly yet

## Current public snapshot

### Historical baseline
- **KDAT-001A** — single-machine governed retrieval baseline
- **KDAT-002** — operator workflow layer over governed retrieval

### Ready to publish from current branch evidence
- **KDAT-003**
- **KDAT-008**
- **KDAT-012**
- **KDAT-013**
- **KDAT-014**
- **KDAT-015**
- **KDAT-016**
- **KDAT-017**
- **KDAT-018**
- **KDAT-019**
- **KDAT-021**

That gives a current public snapshot of **13 ready-to-publish milestones**:
- **2 historical baselines**
- **11 proven on current branch**

### Not yet safe to present as proven
Some milestones are intentionally tracked but remain:
- curated-summary only
- doc-only
- or still under review

Those stay visible in the milestone ledger, but they are not presented as proven technical delivery.

## Start here

| Repo | Purpose |
|---|---|
| [keystone-kdat](https://github.com/getkeystone/keystone-kdat) | Public milestone ledger. Start here for proven vs planned capability history. |
| [keystone-docs](https://github.com/getkeystone/keystone-docs) | Architecture, ADRs, threat model, and supporting documentation. |
| [keystone-core](https://github.com/getkeystone/keystone-core) | Retrieval and query pipeline. |
| [keystone-gov](https://github.com/getkeystone/keystone-gov) | Query-time authorization and tamper-evident audit subsystem. |
| [keystone-console](https://github.com/getkeystone/keystone-console) | Operator-facing workflow and trust-oriented console UX. |
| [keystone-deploy](https://github.com/getkeystone/keystone-deploy) | Reproducible packaging for offline and on-prem deployment. |

## How to read the public milestone ledger

The public ledger is designed to prevent overclaiming.

Each milestone page distinguishes:
- what is proven
- what it does **not** prove
- evidence class
- publication readiness

Evidence classes include:
- **Historical baseline**
- **Proven on current branch**
- **Curated summary**
- **Doc-only reference**
- **Underdocumented**

That distinction is deliberate. Public trust is more important than making the roadmap look bigger than it is.

## What Keystone AI is proving

Keystone AI is aimed at governed operational retrieval for environments where the answer must be:
- grounded in approved source material
- access-controlled at query time
- fail-closed when evidence is insufficient
- auditable after the fact
- operable on customer-controlled infrastructure

## Contact

- **Website:** [getkeystone.ai](https://getkeystone.ai)
- **Milestone ledger:** [keystone-kdat](https://github.com/getkeystone/keystone-kdat)
- **LinkedIn:** [Arnaldo Sepulveda](https://linkedin.com/in/arnaldo-sepulveda)
- **Email:** arnaldo@getkeystone.ai

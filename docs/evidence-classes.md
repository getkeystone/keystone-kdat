# Evidence Classes

Every milestone page in this ledger carries an evidence class. The evidence
class tells you how much you should trust the capability claim on that page.

This matters because milestones in this ledger come from multiple sources:
direct delivery commit history, human-curated summaries, documentation
references, and historical notes. These are not equally credible, and
conflating them produces misleading claims.

---

## Proven on current branch

**What it means:** One or more delivery commits exist on the tracked
development branch (lrfd-backend-bootstrap), naming this milestone explicitly.
Test scripts and/or smoke locks are cited. The commit SHAs are recorded in
the delivery log.

**What it does NOT mean:** The capability is production-ready, deployed at
scale, or validated against an external benchmark. "Proven" here means the
specific technical behavior was built and a test verified it at the time of
the commit.

**When to use in external claims:** Safe to describe the capability as
"built and tested" or "demonstrated on development branch." Do not say
"production-ready" or "enterprise-grade" unless a separate milestone proves
those properties.

---

## Historical baseline

**What it means:** The milestone predates the current tracked branch. It is
referenced in README files or documentation as already established work that
later milestones build upon. No branch commits deliver this milestone in the
current log.

**What it does NOT mean:** The implementation is still current, unchanged, or
representative of the current system state. Historical baselines may have been
refactored, extended, or deprecated by later work.

**When to use in external claims:** Safe to reference as a prior proof point
or baseline. Phrase as "established prior to current development branch" or
"initial proof of concept." Do not present as current delivered state.

---

## Curated summary

**What it means:** A human-authored summary describes this milestone. No
delivery commits for this milestone appear in the current branch commit log.
The description is based on notes, planning documents, or narrative summaries,
not code commit evidence.

**What it does NOT mean:** The capability was never built or does not exist.
It means this ledger cannot verify it from branch commit evidence alone.

**When to use in external claims:** Treat with caution. A curated summary
describes what was intended or reportedly built, not what is directly
verifiable from this evidence log. Mark explicitly if citing externally:
"described in curated summary; not independently verified from commit
evidence."

---

## Doc-only reference

**What it means:** The milestone name or concept appears in documentation
(demo scripts, ops runbooks, README sections), but no dedicated technical
delivery commit is tagged to this milestone number on the current branch.

**What it does NOT mean:** Nothing was built. It means the delivery commit,
if it exists, is not distinctly marked with this KDAT number.

**When to use in external claims:** Do not cite as a technical capability
delivery. Cite only as "referenced in documentation." The underlying
capability may exist but is not independently verifiable from commit
evidence.

---

## Underdocumented

**What it means:** Some evidence exists — a commit reference, a passing
mention, partial documentation — but it is insufficient to fully characterize
what was built or proven.

**When to use in external claims:** Do not cite externally until the milestone
page is upgraded to a higher evidence class. Note as "underdocumented" if
referenced.

---

## Unknown

**What it means:** The milestone appears in a milestone list or index, but
there is insufficient evidence to determine status, what was built, or
whether it was delivered.

**When to use in external claims:** Do not cite. Treat as planned or future
work until evidence is provided.

---

## Why this matters

Many technology milestones suffer from evidence inflation: a curated summary
gets treated as a delivery proof, a demo script reference gets treated as
a tested capability, a planned milestone gets listed alongside proven ones.

This ledger is designed to prevent that. The evidence class is the first
thing to check on any milestone page. If the evidence class is below
"Proven on current branch," external claims must be qualified accordingly.

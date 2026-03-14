# Publication Policy

This document defines the rules governing what can be published from this
milestone ledger and how claims must be framed.

---

## Hard rules

1. Every public claim must map to a milestone page in this ledger.

2. Every milestone page must distinguish what is proven from what remains
   out of scope or unproven.

3. Historical baseline, branch-evidenced delivery, and curated summary must
   never be conflated. They are different evidence classes with different
   credibility.

4. Curated summary is not proof. It is a narrative description that has not
   been independently verified from commit evidence.

5. Doc-only is not delivered technical capability. A reference in a demo
   script does not constitute a working implementation.

6. Unknown stays Unknown until evidence is provided. Gaps must not be
   silently filled with optimistic language.

7. Do not use the following terms unless a milestone explicitly proves them:
   - enterprise-ready
   - enterprise-grade
   - production-ready
   - production-hardened
   - highly available (HA)
   - disaster recovery (DR)
   - multi-node
   - OIDC
   - ABAC
   - zero-trust
   - SOC 2 compliant
   - HIPAA compliant

8. Do not publish raw internal material: commit log dumps, internal hostnames,
   private URLs, collaborator notes, ops identifiers, or personal information.

9. Prefer derived public summaries over verbatim internal content.

---

## Preferred language

| Instead of | Use |
|------------|-----|
| "enterprise-ready" | "built and tested at demonstration scale" |
| "production hardened" | "validated on development branch with smoke tests" |
| "proven at scale" | (only if a scale milestone exists) |
| "supports OIDC" | (omit unless a milestone proves it) |
| "deployed in production" | (omit unless deployment evidence exists) |
| "fully tested" | "covered by N test assertions in listed test scripts" |

Use:
- "proves today" for branch-evidenced claims
- "historical baseline" for pre-branch established work
- "validated on branch" for smoke-locked behavior
- "next planned step" for future work
- "curated summary" when citing non-branch-evidenced milestones

---

## Before publishing a milestone reference externally

Checklist:
- [ ] Does the milestone page exist in this ledger?
- [ ] Is the evidence class Proven on current branch or Historical baseline?
- [ ] Have you read the "does NOT prove" section?
- [ ] Does your claim stay within the "public-safe claims" section?
- [ ] Does your claim avoid the prohibited language list?
- [ ] Is the milestone's publication status "Ready to publish"?

If any answer is no, do not publish the claim until the gaps are resolved.

---

## Publication status values

| Status | Meaning |
|--------|---------|
| Ready to publish | Page is complete, evidence class is appropriate, no prohibited claims |
| Needs review | Content exists but requires human review before external use |
| Stub only | Page exists as a placeholder; content is insufficient for any claim |
| Not publishable yet | Evidence is too thin or risks overclaiming |

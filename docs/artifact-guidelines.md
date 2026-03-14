# Artifact Guidelines

Artifact folders in [artifacts/](../artifacts/) contain public-safe evidence
summaries for milestones where shareable artifacts exist or are planned.

---

## What goes in an artifact folder

- Public-safe descriptions of what the artifact is
- What the artifact proves and what it does not prove
- The publication readiness of the artifact
- A pointer to where a public-safe version should be hosted

## What does NOT go in an artifact folder

- Raw internal test output dumps
- Private hostnames or infrastructure paths
- Credentials or secrets of any kind
- Internal collaborator notes
- Unreviewed commit log excerpts

---

## Artifact publication readiness

Each artifact folder README should state one of:

- **Ready** — artifact can be shared externally as described
- **Needs sanitization** — artifact exists but requires redaction before sharing
- **Planned** — artifact described but not yet produced
- **Not applicable** — no shareable artifact is appropriate for this milestone

---

## Creating a new artifact entry

1. Create a folder under `artifacts/kdat-NNN/`
2. Add `README.md` with the standard template (see [milestone-template.md](milestone-template.md))
3. State clearly: what the artifact is, what it proves, what it does not prove,
   and its publication readiness
4. Do not include the artifact file itself unless it has been sanitized and reviewed

# 01 — Multi-Document Pool

> Framework invoked by Step 1 of the main flow (`SKILL.md`).
> Resolves one or multiple source documents into a single, deduplicated
> experience pool that serves as the ground truth for the One Pager.

---

## Inputs

- One or more experience documents loaded by the user or available in Project
  Knowledge: CVs, résumés, previous One Pagers, LinkedIn exports.

If no experience document is available, request one before proceeding. Do not
build a One Pager from the JD alone.

---

## Process

### A. Detect how many documents are present

Count the distinct experience documents available (in the chat and in Project
Knowledge). A photo and a JD are not experience documents.

### B. If a single document

Use it directly as the pool. Proceed to onboarding (Moment 1) or tailoring.

### C. If multiple documents — ask about a primary

> "You've loaded [N] documents. Is there one you consider the primary CV, or
> should I treat them all equally and build a unified pool?"

- **Primary indicated:** use it as the base. Pull from the others only where
  they add something the primary doesn't cover.
- **No primary:** treat all documents with equal weight.

### D. Build the unified pool

Extract experiences, skills, certifications, and contact details from all
documents in scope, without duplicating. When the same experience appears in
more than one document:

- Use the most specific version (more detail, metrics, scope) over the thinner one.
- When detail is comparable, use the most recent version.
- If two documents conflict on a fact (different dates, titles, numbers), do not
  silently pick one. Flag it to the user and ask which is correct.

The resulting pool is the single source of truth for this session. Nothing may
appear on the One Pager that isn't in the pool or confirmed by the user during
onboarding or gap translation.

---

## Output

A unified experience pool ready for tailoring, plus a note of which document
contributed which material when multiple were used. This source attribution
feeds the change note (see `frameworks/04-tailoring.md`).

---

## Quality rules

- **No duplication.** The same experience must not appear twice because it was in
  two documents.
- **No silent conflict resolution.** Conflicting facts across documents are
  surfaced to the user, never resolved by guessing.
- **Source traceability.** When non-primary material is used, record where it
  came from so it can be declared in the change note.
- **Truthfulness carries through.** The pool inherits the global truthfulness
  rule from `SKILL.md`: it defines what is *available*, not what *must* appear.
  Selection happens later, in tailoring.

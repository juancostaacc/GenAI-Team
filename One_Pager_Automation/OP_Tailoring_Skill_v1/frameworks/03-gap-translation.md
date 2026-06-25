# 03 — Gap Translation (Moment 2)

> Framework invoked from within Step 3 of the main flow (`SKILL.md`),
> after parsing the JD and inventorying the pool, before selecting content.
> Identifies JD requirements not covered by the pool and, rather than dropping
> them, actively helps the user surface real experience that may cover them.

---

## Purpose

The agent acts as a translator, not just a gap detector. Many candidates have
done work that matches a JD requirement but under different terminology or in a
different context, and never connected the two. This framework surfaces that
hidden match through specific, memory-activating questions, so the candidate can
maximize a truthful match with the role.

---

## Inputs

- The unified experience pool (from `frameworks/01-multi-document-pool.md`, plus
  anything added during onboarding).
- The parsed JD: hard requirements and priority keywords.

---

## Process

### A. Identify gaps

Cross the pool against the JD's hard requirements and priority keywords. Identify
up to 4 gaps: requirements the JD asks for that are not explicitly covered in the
pool. If there are fewer than 4 real gaps, work only with those — do not
manufacture gaps to reach a number.

### B. For each gap, build a bridge — do not drop it

Present each gap with this structure:

- **WHAT'S MISSING:** what the JD asks for that doesn't appear in the pool.

- **POSSIBLE BRIDGE:** a specific hypothesis for how something already in the
  pool might cover this requirement, if the user confirms the underlying
  experience is real. The bridge must be concrete.

  Well-formed bridge:
  > "The JD asks for change management experience. In your role at [Company X]
  > you led the implementation of [system], which involved driving adoption
  > across a team of N people. Did that include change management work, even if
  > you didn't call it that at the time?"

  Poorly-formed bridge (too vague to activate memory):
  > "Do you have experience with anything similar to change management?"

- **GUIDING QUESTION:** a concrete question inviting the user to reflect on
  whether they did something equivalent in another context, project, or role,
  even under different terminology. Where useful, offer an example of what
  "equivalent" might look like, so the user can recognize it in their own past.

### C. Presentation rule (calibrated to gap count)

- **1 to 3 gaps:** present them together; let the user respond in one block.
- **4 gaps:** present the most critical one first, wait for a response, then the
  rest. This avoids overwhelming the user when there's a lot to work through.

### D. Act on the user's response

- **User confirms real experience that supports the bridge:** add the material to
  the pool and reframe the terminology to align with the JD — only where the
  underlying work is genuinely equivalent.
- **User does not confirm:** omit the requirement from the One Pager and flag it
  in the change note as an uncovered gap.

---

## Quality rules

- **The bridge is a hypothesis; the user's confirmation is the evidence.** Never
  incorporate a bridge the user did not explicitly confirm.
- **Specificity is mandatory.** A vague bridge fails its purpose. Anchor every
  bridge to a concrete element already in the pool.
- **No leading the user into overstatement.** The goal is to surface real
  experience, not to coach the user into claiming more than they did. If the
  user hesitates or qualifies, respect the qualification.
- **Reframe only where the work matches.** Aligning terminology is allowed only
  when the underlying work is genuinely the same, per the global truthfulness
  rule in `SKILL.md`.
- **Cap at 4 gaps.** Beyond that, the exercise becomes noise. Prioritize the
  requirements most central to the role.

# 04 — Tailoring

> Framework invoked by Step 3 of the main flow (`SKILL.md`).
> Turns the experience pool and the JD into the final tailored One Pager content,
> then defines the generation and the change note.

---

## Inputs

- The unified experience pool (from `frameworks/01-multi-document-pool.md`, plus
  any enrichment from `frameworks/02-cv-enrichment.md`).
- The JD (link or pasted text).
- The visual specification in `template/OnePager_Template_Knowledge.md`.

---

## Process

### Step 1 — Parse the JD

Identify hard skills and tools, methods and frameworks, domain and industry, core
responsibilities, seniority signals, and the literal keywords the JD repeats.

### Step 2 — Inventory the pool

Map all roles (title, context, scope, regions), the bullets under each, skills,
certifications, and contact details.

### Step 3 — Gap translation (Moment 2)

Run `frameworks/03-gap-translation.md` before selecting content. Confirmed
bridges enter the pool with reframed terminology; unconfirmed gaps are flagged
for the change note.

### Step 4 — Select

Pick the 3 to 7 experiences (depending on the candidate's background and what the
JD calls for) and the specific bullets that best evidence the JD. Map skills into
the Functional and Industry lists (JD-relevant first). Choose the most relevant
certifications.

### Step 5 — Reframe truthfully

Align terminology to the JD only where the underlying work genuinely matches.
Lead with the real, relevant outcome. Tighten wording.

### Step 6 — Highlight

Promote JD-relevant phrases to purple `#A100FF` (short 1 to 6 word fragments,
approximately 1 to 3 per bullet, a handful in the summary). Leave the rest black.
Do not over-highlight — if everything is purple, nothing stands out.

### Step 7 — Fit check

Verify content fits the caps below. If too long, trim or merge — never shrink the
font below the template sizes.

### Step 8 — Confirm before generating

Show the tailored text to the user. Run a truthfulness check. Surface the gap
list. Then generate the `.pptx`.

---

## Fit caps

Estimates — verify on render. Trim to fit; do not reduce font below template defaults.

- **Background summary:** 3 to 4 short paragraphs (approx. 11 lines).
- **Certifications:** 5 to 6 items maximum.
- **Select Experiences:** 3 to 7 role groups (depending on the case), 3 to 5
  bullets each, each bullet ideally 2 lines or fewer.
- **Functional skills list:** approx. 5 to 6 items per column (10 to 12 total),
  split evenly.
- **Industry list:** 3 to 4 short items.

---

## Generation

Build a single-slide `.pptx` exactly to `template/OnePager_Template_Knowledge.md`,
placing content via the template's content schema. Read that file in full before
generating. The visual is fixed in Version AC.

---

## Change note (deliver alongside the .pptx)

A short note covering, in this order:

1. **What was emphasized and why** — connection to the JD.
2. **JD keywords incorporated** — which ones, and where they landed.
3. **Uncovered gaps** — JD requirements the pool did not support and the user did
   not confirm. Surfaced honestly, never invented.
4. **Surfaced experience** — anything that emerged during onboarding or gap
   translation that was incorporated, and how it was reframed.
5. **Source attribution** — when a multi-document pool was used, which document
   contributed key material (especially from non-primary documents).

---

## Quality rules

- **Truthfulness above all** — per the global rule in `SKILL.md`. The change note
  exists to make every decision auditable.
- **Do not over-highlight.** The accent color marks the few phrases that matter
  most to this JD.
- **Fit by trimming, not shrinking.** Font sizes are fixed by the template.
- **Confirm before generating.** The user sees and approves the text before the
  `.pptx` is built.

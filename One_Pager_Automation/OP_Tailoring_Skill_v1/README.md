# AC_OP_tailoring

A Claude skill that tailors your **One Pager** (a single-slide CV summary) to a
specific job opportunity and produces it as a ready-to-use `.pptx`, on a fixed
visual template.

It is not a generic résumé generator. It works at the content level, not the
formatting level: it reads your real experience, surfaces what's relevant to the
role, and translates work you've done but never connected to the JD's language —
without ever inventing anything.

---

## How it works

Given your experience documents and a job description, the agent:

1. **Resolves your experience into one pool.** Your background can be spread
   across different CVs, old One Pagers, or a LinkedIn export. Load them all; the
   agent reads them as a single deduplicated pool, uses the most specific or
   recent version when something appears twice, and flags conflicts instead of
   guessing.
2. **Enriches thin documents (optional).** If your material lacks metrics, scope,
   or detail, a short skippable round of questions surfaces what's missing before
   tailoring.
3. **Translates gaps instead of dropping them.** When the JD asks for something
   your documents don't show, the agent doesn't silently omit it. It proposes a
   specific bridge ("you did X at Company Y — isn't that what the JD calls Z?")
   and asks, so you can claim real experience you'd otherwise leave on the table.
4. **Selects and reframes.** Picks the most relevant experiences (typically 3 to
   7, depending on your background and the role) and aligns their wording to the
   JD where the underlying work genuinely matches.
5. **Highlights and generates.** Marks JD-relevant phrases in the template's
   accent color, builds the `.pptx`, and delivers a change note: what was
   emphasized, which keywords were used, what gaps remain, and where each piece of
   material came from.

The visual design is fixed. The words change. Nothing is invented — every output
is supported by your documents or confirmed by you in the session. Uncovered JD
requirements are flagged as gaps, never fabricated.

---

## What you need to bring

For each session:

1. **Your experience documents** — one CV, or several (CVs, previous One Pagers,
   LinkedIn exports).
2. **A headshot photo** — square crop, approx. 1.22 inches.
3. **The job description** — link or pasted text.

The agent asks for whatever is missing before it starts.

---

## Installation

### Prerequisites

- A Claude account (Free, Pro, Max, Team, or Enterprise).
- **Code execution and file creation** enabled: in Claude.ai, go to
  **Settings → Capabilities** and turn it on. Without this the skill cannot
  generate files.

### In Claude.ai (web or desktop)

1. Get the `.zip`: use the file you received directly, or download the latest
   version from the
   **[Releases](https://github.com/GenAI-Team/AC_OP_tailoring/releases)** page.
2. In Claude.ai, go to **Customize → Skills**.
3. Click **"+"** → **"+ Create skill"** → **"Upload a skill"**.
4. Select the `.zip` you downloaded.
5. Enable the skill with the toggle. It's now available in any chat.

### In Claude Code

Clone the repo, or unzip the `.zip` into your skills folder:

```bash
# from GitHub
git clone https://github.com/GenAI-Team/AC_OP_tailoring ~/.claude/skills/AC_OP_tailoring

# or from the zip you received
unzip AC_OP_tailoring.zip -d ~/.claude/skills/
```

Claude Code auto-detects the skill on next start.

---

## Recommended use — flow with Projects (Pro+)

The cleanest flow uses a Claude **Project** to keep your experience documents
always loaded, so you only bring the JD each time.

1. Install the skill.
2. **Create a new Project** in Claude.ai. Name it "One Pager" or whatever you prefer.
3. Go to **Project Knowledge** and upload your experience documents and photo there.
4. To tailor for a role, open a new chat inside the Project and say:

   > "Tailor my One Pager for this role. JD: [link or pasted text]."

5. The agent runs the full flow and delivers the `.pptx` with a change note.
6. When your experience changes, upload the new document to Project Knowledge,
   replacing the outdated one.

**Free plan (without Projects):** the skill works the same, you just attach your
documents and photo in each chat instead of having them persist in a Project.

**Updating the skill:** personal skills don't update in place. In
**Customize → Skills**, delete the old `AC_OP_tailoring`, then upload the new
`.zip`. Your Project Knowledge is not affected — only the skill code is replaced.

---

## Repository structure

```
AC_OP_tailoring/
├── SKILL.md                            # Orchestrator (role, flow, truthfulness rule)
├── frameworks/
│   ├── 01-multi-document-pool.md       # Resolve one or many documents into one pool
│   ├── 02-cv-enrichment.md             # Lightweight onboarding (Moment 1)
│   ├── 03-gap-translation.md           # Gap translation (Moment 2, the differentiator)
│   └── 04-tailoring.md                 # Tailoring steps, fit caps, generation, change note
├── template/
│   └── OnePager_Template_Knowledge.md  # Fixed visual specification of the One Pager
├── docs/                               # Documentation assets (optional)
└── README.md
```

---

## Stated limitations

- **The visual template is fixed in this version (AC).** A future version
  (currently in design) will let you define your own template.
- **It's as good as the material you bring.** With thin documents and skipped
  enrichment, the One Pager can only reflect what little it was given.
- **It tailors, it doesn't write your career.** The agent selects, translates, and
  formats real experience. It won't invent achievements or decide which roles to
  apply for.

---

## Acknowledgments

The enrichment and gap-translation methodology in this skill was inspired by the
interview preparation framework developed by
[@martinjbellocq](https://github.com/martinjbellocq) in the
[full-interview-prep](https://github.com/martinjbellocq/full-interview-prep)
project. That work shaped how this agent thinks about surfacing and translating
experience across contexts.

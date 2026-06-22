# One Pager Tailoring Agent

A Claude skill that tailors your One Pager (a single-slide CV summary) to a
specific job opportunity and produces it as a ready-to-use `.pptx` file.

The visual design is fixed. The words change. Every output is honest, specific,
and calibrated to the role — not a generic résumé dressed up as a slide.

---

## What it does

Given your experience documents and a job description, the agent:

1. Parses the JD for hard skills, keywords, seniority signals, and implicit
   priorities.
2. Inventories your experience pool across one or multiple documents.
3. Identifies gaps between what the JD asks and what's documented — and before
   skipping them, asks targeted questions to surface real experience you may not
   have connected to the requirement.
4. Selects the 2 to 3 most relevant experiences and reframes them truthfully to
   match the JD's language.
5. Highlights JD-relevant phrases in the template's accent color.
6. Generates the `.pptx` and delivers a change note explaining every decision.

Nothing is invented. Everything in the output is supported by your documents or
confirmed by you during the session.

---

## What you need to bring

- **Your experience documents** — one CV, or multiple (CVs, previous One Pagers,
  LinkedIn exports). The agent reads them as a unified pool.
- **A headshot photo** — square crop, approx. 1.22 inches.
- **The job description** — link or pasted text.

That's it for each session. The agent asks for whatever is missing.

---

## Installation

### Prerequisites

- A Claude account (Free, Pro, Max, Team, or Enterprise).
- **Code execution and file creation** enabled: go to **Settings → Capabilities**
  in Claude.ai and turn it on. Without this the skill cannot generate files.

### Steps

1. Download the `.zip` from the [Releases](../../releases) page.
2. In Claude.ai, go to **Customize → Skills**.
3. Click **"+"** → **"+ Create skill"** → **"Upload a skill"**.
4. Select the `.zip` you downloaded.
5. Enable the skill with the toggle.

The skill is now available in any chat.

---

## Recommended setup — Claude Projects (Pro and above)

The skill handles the logic. A Claude Project handles the persistence of your
personal material. Together, they give you the best experience.

**One-time setup:**

1. Install the skill following the steps above.
2. Create a new Project in Claude.ai. Name it whatever you like ("One Pager",
   "Job Search", etc.).
3. Go to **Project Knowledge** and upload your experience documents (CVs, previous
   One Pagers) and your photo there.
4. From now on, every chat you open inside the Project has your material available
   automatically. You only need to bring the JD.

**Each time you tailor for a new role:**

1. Open a new chat inside the Project.
2. Paste or link the JD.
3. The agent runs the full tailoring flow and delivers the `.pptx` with a change
   note.

**When to update Project Knowledge:**

- You have a new or updated CV.
- You want to add a new One Pager as an additional source.
- Your photo changes.

Simply upload the new file to Project Knowledge (and remove the outdated version
if replacing it).

---

## Alternative setup — Free plan (without Projects)

If you don't have a Pro plan, you can still use the skill — with a small amount
of extra friction each session:

1. Install the skill.
2. For each tailoring session: open a new chat, **attach your experience
   documents** and photo, and paste the JD.
3. The agent runs the full flow normally.

The output quality is identical. You just need to re-attach your documents each
time instead of having them persist in a Project.

---

## Working with multiple experience documents

If your experience is spread across different CVs or One Pagers (for example, one
oriented toward operations and another toward strategy, or one per industry), load
them all. The agent:

- Asks if one of them is your primary document or if it should treat them equally.
- Builds a unified pool from all documents, without duplicating.
- When the same experience appears in more than one document, uses the most
   specific or most recent version.
- Notes in the change note when material from a non-primary document was used.

No manual consolidation needed.

---

## What's fixed in this version (AC)

The visual template is fixed. The slide layout, coordinates, palette, fonts, and
embedded image assets are defined in `OnePager_Template_Knowledge.md` and do not
change between outputs. If you want to use a different visual format, a future
version of the skill (currently in design) will support custom templates.

---

## Updating the skill

When a new version is released:

1. Check the [CHANGELOG](CHANGELOG.md) to see if the changes are relevant to you.
2. Download the new `.zip` from Releases.
3. In **Customize → Skills**, find `one-pager-tailoring`, click the three dots
   (**...**), and select **Delete**.
4. Upload the new `.zip` following the installation steps.

Your experience documents in Project Knowledge are not affected by skill updates.

---

## Repository structure

```
one-pager-tailoring/
├── SKILL.md                        # Agent logic and instructions
├── OnePager_Template_Knowledge.md  # Visual specification of the One Pager
├── README.md
├── CHANGELOG.md
└── LICENSE
```

---

## Acknowledgments

The enrichment and gap translation methodology in this skill was inspired by the
interview preparation framework developed by
[@martinjbellocq](https://github.com/martinjbellocq) in the
[full-interview-prep](https://github.com/martinjbellocq/full-interview-prep)
project. That work shaped how this agent thinks about surfacing and translating
experience across contexts.

---

## License

MIT. See [LICENSE](LICENSE).

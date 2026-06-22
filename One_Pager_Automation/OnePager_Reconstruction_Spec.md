# Accenture One Pager — Visual Reconstruction Spec

A complete, build-ready specification for reproducing the "One Pager" (single-slide CV) layout pixel-for-pixel, then dropping in role-tailored text. Every coordinate, color, font size, bullet, and asset below was extracted directly from the source file `Nuevo_OP.pptx` (the Ritika Saraswat example). The intent is that an artifact (e.g. a browser tool using **PptxGenJS**) can read this spec and emit a faithful `.pptx`.

> **Source of truth & confidence.** All geometry, colors, fonts, sizes, and bullet definitions in the tables below are read straight from the file's XML — treat them as confirmed. The few items I derived or substituted are explicitly flagged with ⚠️ and a recommendation. Where I say "verify against the reference," it means render your output and eyeball it next to the original, because I could not confirm that detail with certainty.

---

## 1. Canvas

| Property | Value |
|---|---|
| Slide size | **13.333 in × 7.5 in** (16:9 widescreen, `LAYOUT_WIDE`) |
| EMU per inch | 914400 (source stores everything in EMU; this doc reports inches) |
| Background | White `#FFFFFF` |
| Single slide | Yes — the One Pager is always exactly one slide |

All `x / y / w / h` values below are **inches from the top-left corner**.

---

## 2. Color palette

| Token | Hex | Used for |
|---|---|---|
| **Primary purple** | `#A100FF` | Inline keyword/impact highlights inside body text; hyperlink text (email, LinkedIn); the `>` chevron mark; the photo-frame square |
| **Title purple** | `#7500C0` | Person name; the three section headers (`BACKGROUND`, `SELECT EXPERIENCES`, `EXPERTISE`) |
| **Deep violet** | `#3A00A1` | Contact icon fill (phone/email) |
| **Body black** | `#000000` | Default body text, practice line, role line, certifications, functional list |
| **Muted text** | `#333333` | Industry list items only |
| **Divider gray** | `#808080` | Dashed separator lines ⚠️ (see note) |

⚠️ **Divider gray is derived.** In the file the dashed lines use the theme "Background 1" color at 50% luminance. In a standard Office theme Background 1 is white, so 50% luminance resolves to a mid-gray ≈ `#808080`. I recommend `#808080` (or `#7F7F7F`) but suggest you verify against the reference render.

⚠️ **Minor source inconsistency.** A couple of highlighted runs in the original use `#A000FF` instead of `#A100FF` (almost certainly an authoring typo — the two are visually identical). Standardize everything on **`#A100FF`**.

---

## 3. Typography

**Font family: Arial** for 100% of the text (a safe, metric-stable font). Use `fontFace: "Arial"` everywhere.

| Element | Size (pt) | Weight | Color |
|---|---|---|---|
| Person name | 20 | Bold | `#7500C0` |
| Practice / industry line | 14 | Bold | `#000000` |
| Role / title line | 16 | Bold | `#000000` |
| Section headers (BACKGROUND / SELECT EXPERIENCES / EXPERTISE) | 12 | Bold | `#7500C0` |
| Sub-headers (Functional / Industry) | 10 | Bold | `#000000` |
| Background summary body | 10 | Regular | `#000000` (+ `#A100FF` highlights) |
| Certifications — "Certifications:" label | 10 | Bold | `#000000` |
| Certifications — list items | 10 | Regular | `#000000` |
| Phone text | 10 | Regular | `#000000` |
| Email / LinkedIn text | 9 | Regular | `#A100FF` |
| Experience — role/context header line | 9 | Bold | `#000000` |
| Experience — bullet text | 9 | Regular | `#000000` (+ `#A100FF` highlights) |
| Expertise — Functional items | 9 | Regular | `#000000` |
| Expertise — Industry items | 9 | Regular | `#333333` |
| Footer copyright | ~8–9 | Regular | gray |

---

## 4. The inline-highlight rule (the core "tailoring" mechanic)

This is what makes the One Pager feel impact-driven. Inside the **Background summary** and every **experience bullet**, the text is a mix of two run colors:

- Default narrative text → **black `#000000`**
- Selected impact phrases (strong verbs, outcomes, metrics, named methods/tools) → **purple `#A100FF`**

So each paragraph is not a single string — it is an **ordered list of runs**, each with its own color (and occasionally bold). When tailoring to a role, the tool decides which phrases to promote to purple. Keep highlights to short, meaningful fragments (1–6 words), not whole sentences.

In PptxGenJS this maps to the **text-array form**:
```js
slide.addText([
  { text: "Led the re-baselining of project scope, spearheading cross-functional ", options: { color: "000000" } },
  { text: "\"pod\" refinements", options: { color: "A100FF" } },
  { text: " to ensure technical alignment.", options: { color: "000000" } },
], { /* box position + bullet options */ });
```

---

## 5. Element layout map

Coordinates are exact (inches). "Box" = a text frame unless noted. Boxes with internal padding note it; unless stated, internal margins are **0** (`lIns/tIns/rIns/bIns = 0`).

### 5.1 Header band

| # | Element | x | y | w | h | Notes |
|---|---|---|---|---|---|---|
| 1 | `>` chevron mark | 0.156 | 0.142 | 0.21 | 0.221 | Image asset (`CHEVRON`), purple. Top-left corner. ⚠️ verify size vs reference |
| 2 | Photo-frame square | 0.468 | 0.403 | 1.063 | 1.25 | Solid fill `#A100FF`, **no border**. Sits *behind* the photo |
| 3 | Photo | 0.25 | 0.385 | 1.218 | 1.219 | Image (`PHOTO`). In front of #2, offset up-left → purple square peeks out ~0.05–0.06" along the **bottom and right** (the offset-frame motif) |
| 4 | Identity text block | 1.729 | 0.326 | 4.016 | 1.346 | 4 lines: **Name** (20/Bold/`7500C0`) · **Practice line** (14/Bold/black) · *(blank line)* · **Role** (16/Bold/black) |

### 5.2 Divider lines — 0.5 pt, **dashed**, `#808080`

| # | Element | x | y | w | h | Orientation |
|---|---|---|---|---|---|---|
| 5 | Column divider | 5.841 | 0.587 | — | 6.593 | Vertical (separates left/right columns, runs almost full height) |
| 6 | Header underline (left) | 0.548 | 1.773 | 5.328 | 0 | Horizontal, left column only |
| 7 | Expertise/contact divider | 0.548 | 5.754 | 12.556 | 0 | Horizontal, full width |

### 5.3 Left column

| # | Element | x | y | w | h | Notes |
|---|---|---|---|---|---|---|
| 8 | `BACKGROUND` header | 0.55 | 1.833 | 5.197 | 0.297 | 12/Bold/`7500C0` |
| 9 | Background summary body | 0.548 | 2.105 | 5.197 | 2.217 | 10pt run-mixed paragraphs (black + `#A100FF`). No bullets |
| 10 | Certifications block | 0.544 | 4.475 | 5.204 | 1.192 | "Certifications:" bold label, blank line, then bulleted items |
| 11 | Phone icon | 0.48 | 5.799 | 0.253 | 0.206 | Image (`PHONE`) |
| 12 | Phone text | 0.859 | 5.786 | 2.699 | 0.285 | 10/Reg/black |
| 13 | Email icon | 0.506 | 6.184 | 0.219 | 0.158 | Image (`EMAIL`) |
| 14 | Email text | 0.859 | 6.11 | 4.801 | 0.331 | 9/Reg/`A100FF`, hyperlink `mailto:` |
| 15 | LinkedIn icon | 0.462 | 6.506 | 0.29 | 0.295 | Image (`LINKEDIN`) |
| 16 | LinkedIn text | 0.859 | 6.515 | 4.801 | 0.331 | 9/Reg/`A100FF`, hyperlink to profile URL |

### 5.4 Right column

| # | Element | x | y | w | h | Notes |
|---|---|---|---|---|---|---|
| 17 | `SELECT EXPERIENCES` header | 5.922 | 0.321 | 6.852 | 0.297 | 12/Bold/`7500C0` |
| 18 | Experiences body | 5.904 | 0.567 | 7.231 | 5.015 | 9pt. Internal padding: **lIns 0.075", tIns 0.094", rIns 0.0375", bIns 0.095"**. Holds all experience groups (see §6) |
| 19 | `EXPERTISE` header | 5.983 | 5.712 | 6.836 | 0.297 | 12/Bold/`7500C0` |
| 20 | `Functional` sub-header | 5.993 | 5.958 | 2.126 | 0.297 | 10/Bold/black |
| 21 | `Industry` sub-header | 11.385 | 5.958 | 2.126 | 0.297 | 10/Bold/black |
| 22 | Functional list — col 1 | 5.99 | 6.263 | 2.843 | 1.241 | 9/Reg/black, "•" bullets |
| 23 | Functional list — col 2 | 8.543 | 6.263 | 2.646 | 1.241 | 9/Reg/black, "•" bullets |
| 24 | Industry list | 11.327 | 6.263 | 1.901 | 0.926 | 9/Reg/`#333333`, "•" bullets |

> The Functional expertise list is split across **two side-by-side columns** (#22, #23). Industry (#24) is a single narrower column on the far right.

### 5.5 Footer (recreate manually — in the original these come from the slide master)

| # | Element | x | y | w | h | Notes |
|---|---|---|---|---|---|---|
| 25 | Copyright | 0.417 | 7.117 | 4.685 | 0.248 | "Copyright © 2026 Accenture. All rights reserved." small gray |
| 26 | Page number | ~12.34 | 7.117 | ~0.58 | 0.248 | "1", bottom-right, gray |

⚠️ The chevron (#1), copyright (#25), and page number (#26) live on the slide **master/layout** in the original, not the slide itself. A from-scratch PptxGenJS build has no master, so **add them as normal shapes** at the coordinates above.

---

## 6. "Select Experiences" structure

The right-hand experiences box (#18) is one text frame containing a repeating pattern:

1. **Role header line** — bold, black, 9pt, **no bullet**. Format: `Role/Title – Context (scope/regions)`. e.g. *"Delivery Lead– MHRA UK (Regulatory Connect Programme)"*.
2. **3–6 impact bullets** — 9pt, square bullet, run-mixed black + `#A100FF` highlights. Each starts with a strong verb and ends in an outcome.
3. **One blank line** separating each role group from the next.

The example has **3 role groups**. Two to three groups is typical; the box height (5.015") comfortably holds ~22–24 lines of 9pt text.

### Bullet style for experiences ⚠️ substitution
The source uses a **Wingdings "§"** character, which renders as a small filled **square ▪**. PptxGenJS bullets are font-dependent, so for a reliable square use a Unicode square instead:
```js
bullet: { code: "25AA" }   // ▪ U+25AA, font-independent square
```
This is a deliberate substitution for portability; it looks the same as the original square. If you want byte-identical behavior, set the bullet character to "§" with `fontFace: "Wingdings"`, but that depends on the viewer having Wingdings.

---

## 7. Bullet & indentation reference

| List | Bullet | Hanging indent (marL = indent magnitude) | Color |
|---|---|---|---|
| Experience bullets (#18) | square ▪ (Wingdings "§" → use `25AA`) | 0.1875 in (13.5 pt) | inherits black |
| Certifications items (#10) | "•" (Arial) | 0.1875 in (13.5 pt) | black |
| Functional expertise (#22/#23) | "•" (Arial, 100%) | 0.118 in (≈8.5 pt) | black |
| Industry expertise (#24) | "•" (100%) | 0.139 in (10 pt) | `#333333` |

All lists use a **hanging indent**: `marL = +value`, `indent = −value` (text wraps flush under the first character, bullet hangs left). No extra paragraph spacing-before/after is set in the source (spacing comes from natural line height); add small `paraSpaceAfter` only if you find lines too tight when you render.

Conversion helpers: `1 in = 914400 EMU = 72 pt`.

---

## 8. PptxGenJS build skeleton

A minimal, faithful starting point. Fill `data` from the role-tailored content; the geometry is locked to §5.

```js
// const pptx = new PptxGenJS();
pptx.defineLayout({ name: "OP", width: 13.333, height: 7.5 });
pptx.layout = "OP";
const C = { primary:"A100FF", title:"7500C0", violet:"3A00A1", black:"000000", muted:"333333", gray:"808080" };
const FONT = "Arial";
const s = pptx.addSlide();

// --- Header ---
s.addImage({ data: A.chevron, x:0.156, y:0.142, w:0.21, h:0.221 });
s.addShape(pptx.ShapeType.rect, { x:0.468, y:0.403, w:1.063, h:1.25, fill:{ color:C.primary } });   // frame square (behind)
s.addImage({ data: A.photo,   x:0.25,  y:0.385, w:1.218, h:1.219 });                                  // photo (front)
s.addText([
  { text: data.name,     options:{ fontSize:20, bold:true, color:C.title } },
  { text: "\n"+data.practice, options:{ fontSize:14, bold:true, color:C.black, breakLine:true } },
  { text: "\n\n"+data.role,   options:{ fontSize:16, bold:true, color:C.black, breakLine:true } },
], { x:1.729, y:0.326, w:4.016, h:1.346, fontFace:FONT, valign:"top", margin:0 });

// --- Dividers (dashed gray) ---
const dash = { color:C.gray, width:0.5, dashType:"dash" };
s.addShape(pptx.ShapeType.line, { x:5.841, y:0.587, w:0, h:6.593, line:dash });
s.addShape(pptx.ShapeType.line, { x:0.548, y:1.773, w:5.328, h:0, line:dash });
s.addShape(pptx.ShapeType.line, { x:0.548, y:5.754, w:12.556, h:0, line:dash });

// --- Section headers ---
const hdr = (t,x,y,w)=> s.addText(t,{ x,y,w,h:0.297, fontFace:FONT, fontSize:12, bold:true, color:C.title, margin:0, valign:"top" });
hdr("BACKGROUND", 0.55, 1.833, 5.197);
hdr("SELECT EXPERIENCES", 5.922, 0.321, 6.852);
hdr("EXPERTISE", 5.983, 5.712, 6.836);

// --- Background summary (run-mixed) ---
s.addText(data.summaryRuns, { x:0.548, y:2.105, w:5.197, h:2.217, fontFace:FONT, fontSize:10, color:C.black, margin:0, valign:"top", lineSpacingMultiple:1.0 });

// --- Experiences: build a runs array, role headers (bold, no bullet) + square bullets ---
s.addText(buildExperienceRuns(data.experiences), {
  x:5.904, y:0.567, w:7.231, h:5.015, fontFace:FONT, fontSize:9, color:C.black, valign:"top",
  margin:[0.094, 0.0375, 0.095, 0.075]  // [top,right,bottom,left] inches
});

// --- Expertise sub-headers + lists ---
s.addText("Functional",{ x:5.993, y:5.958, w:2.126, h:0.297, fontFace:FONT, fontSize:10, bold:true, color:C.black, margin:0 });
s.addText("Industry",  { x:11.385,y:5.958, w:2.126, h:0.297, fontFace:FONT, fontSize:10, bold:true, color:C.black, margin:0 });
const listOpts = (color)=>({ fontFace:FONT, fontSize:9, color, margin:0, valign:"top", bullet:{ code:"2022", indent:8.5 } });
s.addText(data.functionalCol1.map(t=>({text:t})), { x:5.99,  y:6.263, w:2.843, h:1.241, ...listOpts(C.black) });
s.addText(data.functionalCol2.map(t=>({text:t})), { x:8.543, y:6.263, w:2.646, h:1.241, ...listOpts(C.black) });
s.addText(data.industry.map(t=>({text:t})),       { x:11.327,y:6.263, w:1.901, h:0.926, ...listOpts(C.muted) });

// --- Certifications ---
s.addText([
  { text:"Certifications:", options:{ bold:true } },
  { text:"\n", options:{} },
  ...data.certs.map(c=>({ text:c, options:{ bullet:{ code:"2022", indent:13.5 }, breakLine:true } })),
], { x:0.544, y:4.475, w:5.204, h:1.192, fontFace:FONT, fontSize:10, color:C.black, margin:0, valign:"top" });

// --- Contact (icons + linked text) ---
s.addImage({ data:A.phone,    x:0.48,  y:5.799, w:0.253, h:0.206 });
s.addText(data.phone,    { x:0.859, y:5.786, w:2.699, h:0.285, fontFace:FONT, fontSize:10, color:C.black, margin:0, valign:"middle" });
s.addImage({ data:A.email,    x:0.506, y:6.184, w:0.219, h:0.158 });
s.addText(data.email,    { x:0.859, y:6.11,  w:4.801, h:0.331, fontFace:FONT, fontSize:9, color:C.primary, margin:0, valign:"middle", hyperlink:{ url:"mailto:"+data.email } });
s.addImage({ data:A.linkedin, x:0.462, y:6.506, w:0.29, h:0.295 });
s.addText(data.linkedinUrl, { x:0.859, y:6.515, w:4.801, h:0.331, fontFace:FONT, fontSize:9, color:C.primary, margin:0, valign:"middle", hyperlink:{ url:data.linkedinUrl } });

// --- Footer ---
s.addText("Copyright © 2026 Accenture. All rights reserved.", { x:0.417, y:7.117, w:4.685, h:0.248, fontFace:FONT, fontSize:8, color:C.gray, margin:0 });
s.addText("1", { x:12.34, y:7.117, w:0.58, h:0.248, fontFace:FONT, fontSize:8, color:C.gray, align:"right", margin:0 });
```

`buildExperienceRuns()` should, for each group, push the bold role-header run (with `breakLine:true`, no bullet) then each bullet as `{ text, options:{ bullet:{code:"25AA", indent:13.5}, breakLine:true } }` with the bullet's own run array for black/purple highlights, and a blank `{text:"\n"}` between groups.

> ⚠️ PptxGenJS option names (`dashType`, `lineSpacingMultiple`, `bullet.code`, `margin` as `[t,r,b,l]`) should be checked against the version you bundle — the API has shifted across releases. The geometry/colors/sizes above are the authoritative part; the exact JS property spellings are a starting point to verify.

---

## 9. Content schema (what the tool fills per role)

```json
{
  "name": "string",
  "practice": "Public Services - Government Operations",
  "role": "MC Delivery Manager",
  "photo": "data-uri or null (falls back to placeholder)",
  "summaryRuns": [ { "text": "...", "color": "000000|A100FF", "bold": false } ],
  "certs": ["string", "..."],
  "phone": "+91 - XXXXXXXX",
  "email": "name@accenture.com",
  "linkedinUrl": "https://www.linkedin.com/in/...",
  "experiences": [
    {
      "header": "Role – Context (scope/regions)",
      "bullets": [ [ {"text":"...","color":"000000"}, {"text":"highlight","color":"A100FF"} ] ]
    }
  ],
  "functionalCol1": ["string"],
  "functionalCol2": ["string"],
  "industry": ["string"]
}
```

Tailoring guidance for the generator: keep the summary to ~3–4 short paragraphs; 2–3 experience groups with 3–5 bullets each; promote role-relevant skills/tools/outcomes to `#A100FF`; split the Functional list roughly evenly across the two columns; keep Industry to ~3–4 items so it fits the narrower box.

---

## 10. Fidelity checklist (QA after generating)

- Render to PNG and compare side-by-side with the reference.
- Confirm: chevron top-left; purple square peeking bottom-right behind the photo; three purple section headers; vertical divider between columns; full-width divider above the EXPERTISE/contact row.
- Confirm no text overflows its box — the experiences box (#18) is the one most likely to overflow if you add too many bullets; trim content rather than shrink the font below 9pt.
- Confirm highlight purples are `#A100FF` and headers/name are the slightly darker `#7500C0`.
- Confirm contact rows: icon vertically centered against its text line.

---

## 11. Embedded assets (base64 PNG data URIs)

Paste these straight into the tool as `const A = { ... }`. The photo is a neutral placeholder — replace per person.

```js
const A = {
  chevron: "data:image/png;base64,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",
  phone: "data:image/png;base64,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",
  email: "data:image/png;base64,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",
  linkedin: "data:image/png;base64,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",
  photo: "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAlgAAAJYCAYAAAC+ZpjcAAAQoklEQVR4nO3czZHbuBpA0bZrAvKi84/AiwmiF87CbzHlerb7T6IuSQA8JwBbVQQ/XEJUf3l5+fHzCQCAzNezPwAAwGoEFgBATGABAMQEFgBATGABAMQEFgBATGABAMQEFgBATGABAMQEFgBATGABAMQEFgBATGABAMQEFgBATGABAMQEFgBATGABAMQEFgBATGABAMQEFgBATGABAMQEFgBATGABAMQEFgBATGABAMQEFgBATGABAMQEFgBATGABAMQEFgBATGABAMQEFgBATGABAMQEFgBATGABAMQEFgBATGABAMQEFgBATGABAMQEFgBATGABAMQEFgBATGABAMQEFgBATGABAMQEFgBATGABAMQEFgBATGABAMQEFgBATGABAMQEFgBATGABAMQEFgBATGABAMQEFgBATGABAMQEFgBATGABAMQEFgBATGABAMQEFgBATGABAMQEFgBATGABAMQEFgBATGABAMQEFgBATGABAMQEFgBATGABAMQEFgBATGABAMQEFgBATGABAMQEFgBATGABAMQEFgBATGABAMQEFgBATGABAMQEFgBATGABAMQEFgBATGABAMQEFgBATGABAMQEFgBATGABAMQEFgBATGABAMQEFgBATGABAMQEFgBATGABAMQEFgBATGABAMQEFgBATGABAMQEFgBATGABAMQEFgBATGABAMQEFgBATGABAMQEFgBATGABAMQEFgBATGABAMQEFgBATGABAMQEFgBATGABAMQEFgBATGABAMQEFgBATGABAMQEFgBATGABAMT+OfsDADw9PT19//5v9m89P3/L/i2ALb68vPz4efaHAK6hjKitxBdwBIEF7GKEmLqV6AJqAgtIzBRUnxFcwKMEFrDJSkH1GcEF3EtgATe7UlS9R2wBtxBYwKeE1WtCC/iIwALeJKpuJ7aAvwks4A/CajuhBfwisICnpydhVRJagMCCixNW+xFacF0CCy5KWB1HaMH1CCy4GGF1HqEF1yGw4CKE1TiEFqzv69kfANifuBqL6wHrc4IFC7ORj89pFqzJCRYsSlzNwXWCNTnBgsXYsOflNAvW4QQLFiKu5ub6wToEFizC5rwG1xHW4CtCmJwNeV2+MoR5OcGCiYmrtbm+MC+BBZOy+V6D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"   // neutral placeholder; swap in a real cropped square headshot
};
```

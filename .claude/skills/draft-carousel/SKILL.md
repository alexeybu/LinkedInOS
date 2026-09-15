---
name: draft-carousel
description: Take one idea from ideas/backlog.md and turn it into a full LinkedIn carousel post — slide-by-slide copy, a caption, and every slide rendered as a PNG — in drafts/<date>-<slug>-carousel.md and drafts/images/<slug>/. Input: an idea ID (and optionally a slide count, otherwise read from the idea's Format cell). Use when the user wants to draft an actual carousel/document post, as opposed to a single text post (draft-post) or generating ideas/strategy.
---

# Draft Carousel

Takes one real idea tagged `Carousel` (or explicitly requested as one) in `ideas/backlog.md` and
produces the complete deliverable in one pass: slide copy, a caption, and every slide rendered as a
PNG in this workspace's carousel visual style. One skill start to finish — unlike text posts, where
drafting (`draft-post`) and image generation (`post-image`) are separate skills, a carousel's slide
*text* and slide *image* are the same content, so splitting them into two passes would mean writing
each slide's copy twice.

## Interaction style

Same as the other LinkedInOS skills: batch enumerable choices with `AskUserQuestion`, use open chat
for anything that needs real judgment (reacting to a full slide set, picking a hook variant). If the
user already named which idea to draft, skip the picking step and confirm the concept in one line
before proceeding.

## 0. Inputs

- **Idea ID** (required) — if the user didn't name one, read `ideas/backlog.md`, filter to
  `Status: new` rows where the `Format` column starts with `Carousel`, and either recommend one
  (one-line reason) or ask via `AskUserQuestion` if there's no clear standout.
- **Slide count** (optional) — if the user gives one, use it, but cross-check against the idea's own
  `Format` cell (e.g. "Carousel — 6 slides (cover + 4 risks + close)") and flag a mismatch rather
  than silently overriding either number. If the user gives no count, use the backlog row's own
  breakdown as-is.
- Once the idea and slide count are confirmed, update that row's `Status` to `drafting` in
  `ideas/backlog.md`.

## 1. Load constraints

Read, in this order:
- **`voice/style-profile.md`** — tone, rhythm, structural patterns, vocabulary, anti-patterns. Same
  single source of truth `draft-post` uses.
- **`strategy/content-pillars.md`** — confirm the idea's pillar, re-read the **guardrails** (binding:
  anonymize companies, never mention the active search, no product/company criticism, no
  confidential metrics, no coworker names), the **Content Type Preference**, and the **Voice
  Framing** section (general-centric/impersonal for the four primary pillars, first-person kept for
  Job Search & Career Journey).
- **`strategy/trend-notes.md`**, if present — pillar-specific angle notes relevant to this idea.
- **`templates/carousel-post-template.md`** — the file-shape, per-slide word-count rules, and the
  full visual spec (sizes, colors, layout) this skill renders against. Don't improvise a different
  structure or a different visual style than what's documented there; if a change is wanted, that's
  a template update first, applied here second.
- The chosen row in **`ideas/backlog.md`** — concept, angle, format/slide breakdown, source,
  guardrail check. Go back to the cited source material for real specifics rather than inventing
  detail the idea note doesn't already contain — this matters more here than in a text post, since
  each content slide needs enough real substance to fill 50-90 words without padding.

## 2. Carousel mechanics (hard constraints)

Per `templates/carousel-post-template.md`'s Visual spec — don't deviate without a template update:

- **Cover slide is a hook, not a summary**: headline ≤12 words, at most one support line ≤15 words.
  Never a paragraph — if the cover tells the whole story, there's no reason to swipe.
- **Content and close slides carry real substance**: headline ≤10 words, body **50-90 words / 3-5
  sentences**. Pull this from the idea's actual detail (the backlog concept, the cited source, prior
  research already in `trend-notes.md`) — if the source material doesn't support that much on one
  point, that's a sign the point needs its own slide, not invented elaboration to hit a word count.
- **Slide count includes cover + close** on top of the real content items — a 4-point checklist is 6
  slides, not 4.
- **Prefer a sketchy-style schema/diagram over a text-only slide** where a clean visual exists for
  the point (added 2026-09-11, explicit user request). See Section 6a for how to design one and
  when to skip it.
- **No external links** anywhere (caption or slides).
- **En dash (–), not em dash**, throughout.
- **General-centric framing** (no first-person "I") unless the idea's pillar is Job Search & Career
  Journey.
- **The caption is separate copy from the slide text** — it hooks the reader into swiping, it
  doesn't restate every slide. No fixed length target yet (first real carousel); keep it short
  enough to read as an invitation, not a substitute for opening the document. 3-5 hashtags per the
  current unconfirmed default (same caveat `draft-post` carries).

## 3. Calibrate: proven structure, dialed-down intensity

Same calibration `draft-post` applies: a real, specific hook per slide and one clear idea per slide,
but no manufactured urgency, no "this will change how you think about X" superlatives, no
engagement-bait close ("What do you think? 👇"). Modest, confident-but-not-declarative register — if
a line reads like it's trying hard to sound impressive, cut the trying-hard part and keep the
substance.

## 4. Pick the structural template

Cover → (slide count − 2) content slides → close. Identify the underlying shape from the backlog
row's `Angle`/`Format` cells — a flat list, a before/after comparison, a decision tree (e.g.
`pm-rice-ice-decision-rule`'s 2-branch shape), or a Q&A-pair device (e.g. `ai-prompt-per-pm-problem`)
— and structure the slides to match that shape rather than forcing everything into a flat list.

## 5. Write the cover slide hook variants

2-3 different angles (direct-question, bold-claim, plain-statement), each ≤12 words, each
consistent with the chosen template. Note which one you'd lead with and why, but leave the actual
choice open for the user to react to.

## 6. Write all slides

Using the recommended cover hook, write every slide: headline + body per Section 2's word-count
rules, one content point per slide, closing on a compact reframe or plain restatement (never a
question). Anonymize per guardrails as you go.

## 6a. Design a diagram for slides where one earns its place (added 2026-09-11)

For each content/close slide, before accepting a text-only layout, consider whether the point has
a clean visual shape — a before→after pair, a flow between two or three things, a comparison, a
relationship — the way `post-image`'s topic icon already does for single-image posts. If one fits,
build a small schema in the same spirit: simple geometric primitives (boxes, arrows, circles,
dashed vs. solid lines), not a literal illustration or clipart (no lightbulb for "an idea," no
magnifying glass for "analysis"). Think in terms of the slide's actual mechanism: e.g. a filled box
labeled with the wrong owner connected by an arrow to a dashed, crossed-out circle for a
"nobody owns it" slide; two stacked boxes with a struck-through arrow between them for a
"the metric doesn't drive the decision" slide; a clock face with a lagging hand for a staleness
slide. **If no clean single-shape idea fits a given slide, leave it text-only** — a forced or
generic diagram is worse than none, exactly like `post-image`'s icon fallback rule. Not every slide
needs one; the cover slide in particular should generally stay text-only, since it's already
minimal by design (Section 2).

Build the diagram as an SVG fragment (labels in `IBM Plex Sans`, drawing strokes in `#a9702c` at
`stroke-width:3-4`, `fill:none` unless a filled accent shape genuinely helps) sized to roughly
700×300-360 within a `viewBox` that matches those proportions — it renders into the slide's middle
region (between the body text and the footer), which is otherwise empty space. Wrap the drawing
elements in `<g filter="url(#sketchy)">…</g>` — `card-template.html` already defines that filter
(the same hand-drawn `feTurbulence`/`feDisplacementMap` technique `post-image` uses) — don't
hand-simulate roughness in the path coordinates themselves. Text labels inside the diagram go
*outside* the sketchy group (filters distort text into illegibility), plain and small.

## 7. Write the LinkedIn caption

2-4 sentences in the user's real voice (long clause-chained sentences reformatted into short visual
lines), hooks into swiping, ends without an engagement-bait question, 3-5 hashtags.

## 8. Inline authenticity check

Same as `draft-post` Section 7 — re-check against `voice/style-profile.md`'s Anti-Patterns, scan for
generic AI writing tells, confirm the chained-sentence rhythm survived reformatting into short
lines. Apply this to the caption **and** every slide's body text, since both are published copy.
Report what you checked and found, even if nothing's flagged.

## 9. Render every slide

For each slide, copy `card-template.html` (in this skill's directory) to a fresh working file per
slide and fill its placeholders:

| Placeholder | Value |
|---|---|
| `__SLIDE_INDEX__` | this slide's number (1-based) |
| `__SLIDE_TOTAL__` | total slide count |
| `__HEADLINE_SIZE__` | `60` for the cover slide, `54` for every other slide |
| `__HEADLINE__` | this slide's headline |
| `__BODY_SIZE__` | `36` (every slide) |
| `__BODY__` | this slide's body text |
| `__DIAGRAM__` | the raw SVG fragment from Section 6a (sketchy-filtered drawing + plain labels), or an empty string (`""`) if this slide stays text-only |
| `__FOOTER__` | `Swipe through the <N-2> →` on the cover, `Swipe →` on every content slide, empty (`""`) on the close slide |

Render each filled file to PNG with headless Chrome (fall back to Edge if Chrome isn't present):
- `C:\Program Files\Google\Chrome\Application\chrome.exe`
- `C:\Program Files (x86)\Microsoft\Edge\Application\msedge.exe`

```bash
"<browser path>" --headless=new --no-sandbox --disable-gpu --hide-scrollbars \
  --window-size=1080,1080 --virtual-time-budget=4000 \
  --screenshot="<ABSOLUTE output slide-N.png path>" \
  "file:///<ABSOLUTE path to the filled working HTML file>"
```

Same two non-negotiables `post-image` learned the hard way:
- **The `--screenshot` output path must be absolute**, and use forward slashes even on Windows — a
  backslash-joined path can silently write to the wrong filename (the `$var\$var2.png` shell-escaping
  trap) or fail outright.
- **`--no-sandbox` is required** in this environment.

`--virtual-time-budget=4000` gives the Google Fonts stylesheet (Sora + IBM Plex Sans) time to load
before the screenshot fires — don't drop it.

Save each PNG to `drafts/images/<slug>/slide-<N>.png` (create the directory if it doesn't exist).
**Read every rendered PNG back before finishing** — confirm no headline/body text is clipped or
overflowing the canvas, the cover really does read as a hook (not a wall of text), fonts loaded
(Sora bold headline vs. a generic fallback is visible at a glance), the light background/dark
text contrast looks right, and — on any slide carrying a diagram — the shape actually rendered
recognizably (not a broken/empty region) and reads as the concept it's meant to represent, not
abstract clutter. Fix and re-render any slide that doesn't pass this check.

## 10. Save the draft

Write `drafts/<date>-<slug>-carousel.md` following `templates/carousel-post-template.md`'s file
shape exactly: frontmatter (including `image: drafts/images/<slug>/`), source idea reference,
structural template note, cover hook variants, every slide's headline/body, the caption with its
character count, the LinkedIn mechanics check, guardrail check, and the inline authenticity check
results.

Update the idea's row in `ideas/backlog.md` from `drafting` to `drafted`.

## 11. Confirm

Send the user every rendered slide PNG (in order) plus the caption text, and ask for real reaction —
cut, reword, re-hook, resize, regenerate a specific slide. This workspace never posts on the user's
behalf — the deliverable is the drafted files, posting is always manual.

## Ground rules

- Never fabricate detail beyond what the source idea/material actually supports — a content slide
  needing 50-90 words is not license to invent specifics; go back to the cited source, or use fewer,
  more honest words and flag that the slide runs shorter than the target.
- Guardrails in `strategy/content-pillars.md` are binding here, not a style preference.
- Never post/publish on the user's behalf.
- Keep the visual system exactly as documented in `templates/carousel-post-template.md` (sizes,
  colors, layout) unless the user explicitly asks to change it — and if they do, update that
  template file first so it stays the source of truth for this skill's renders, the same way
  `post-image`'s established style lives in its own SKILL.md rather than being reinvented per draft.
- A diagram is optional per slide, never mandatory — a forced or generic one is worse than a clean
  text-only slide. Same rule `post-image` applies to its topic icon: visualize a mechanism the
  content already makes, don't invent a new claim just to have something to draw.
- This skill writes drafts, not final copy carved in stone — expect and invite edits, including
  regenerating individual slides rather than the whole set.

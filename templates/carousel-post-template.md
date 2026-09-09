# Carousel Post Template

Structural template for a LinkedIn carousel/document post, used by the `draft-carousel` skill.
Pairs with `draft-post`'s existing structural templates (take/op-ed, narrative/lesson-learned,
practical/how-to) but adds the per-slide breakdown a single-post draft doesn't need. Mirrors
`drafts/<date>-<slug>.md`'s frontmatter/section conventions so carousel drafts and text-post drafts
stay consistent in `drafts/`.

## Why a carousel is structured differently from a text post

A carousel is read as a sequence of images, not a paragraph — each slide has to stand on its own
at a glance (carousels/documents report ~39% more reach than text posts per
`strategy/trend-notes.md` Format Trends). That means:

- **The cover slide is a hook, not a summary.** One short headline (≤12 words) plus at most one
  short supporting line (≤15 words) — never a paragraph. If the cover tells the whole story, there's
  no reason to swipe. (Finalized 2026-09-09 after review — an earlier draft of this template put a
  full 3-4 sentence paragraph on the cover; cut it down to a single hook line.)
- **Content and close slides carry real substance, not a fragment.** Each one needs roughly
  **50-90 words (3-5 sentences)** of body copy under the headline — enough to actually fill the
  slide rather than leaving it looking sparse, but pulled from the backlog idea's real detail, never
  padded with filler just to hit a word count. If the source material doesn't support that much on
  a given point, that's a sign the point needs a different slide, not invented elaboration.
- **Slide count always includes the cover and the close** on top of the real content items — a
  4-point checklist is 6 slides total (cover + 4 + close), not 4. `ideas/backlog.md`'s `Format`
  column already carries this breakdown per idea; use it rather than re-deriving the count.
- **The LinkedIn caption (the text box under the carousel) is separate copy from the slide text**
  — it hooks the reader into swiping and gives the post its own standalone read for anyone who
  never opens the document; it doesn't just restate the slides verbatim.

## Visual spec (finalized 2026-09-09)

Rendered by `draft-carousel` via `card-template.html` in that skill's directory — square
1080×1080, light background, dark text (deliberately distinct from `post-image`'s dark
serif-quote card, so carousels read as their own format):

| Element | Value |
|---|---|
| Canvas | 1080×1080, padding 80px all sides |
| Background | `oklch(0.965 0.012 75)` — warm ivory |
| Headline font | Sora, bold 700 |
| Headline size — **cover** | **60px** |
| Headline size — **content/close slides** | **54px** |
| Headline color | `oklch(0.18 0.02 50)` — near-black warm charcoal |
| Gap between headline and body | **48px** |
| Body font | IBM Plex Sans, regular 400 |
| Body size — **all slides** | **36px** |
| Body color | `oklch(0.32 0.02 50 / 0.88)` |
| Body length — **cover** | one short hook line only, no paragraph |
| Body length — **content/close** | ~50-90 words / 3-5 sentences |
| Layout | top-weighted (content starts right below the slide-counter row, not vertically centered) — avoids the symmetric dead space a centered block leaves on a mostly-empty canvas |
| Accent bar + footer | bottom-left; footer reads "Swipe through the N →" on the cover, "Swipe →" on middle content slides, empty on the close slide |
| Slide counter | top-right, "N / TOTAL" |

## File shape

```yaml
---
date: <YYYY-MM-DD>
pillar: <pillar name>
status: draft
format: carousel
slide_count: <N>              # total, including cover + close — must match ideas/backlog.md's Format cell
character_count_caption: <N>  # the LinkedIn caption text only, not slide text
calendar_slot: <path/date, or "not yet scheduled">
backlog_id: <idea ID from ideas/backlog.md>
image: drafts/images/<slug>/  # slide-1.png ... slide-N.png, rendered by draft-carousel
---
```

```markdown
# Draft (carousel): <working title>

## Source idea

`ideas/backlog.md` — `<backlog_id>` (<pillar>, <batch>): "<concept text, quoted verbatim>"

## Structural template

Cover → <N-2> content slides (one point per slide) → close. Note the underlying shape — a flat
list, a before/after comparison, a decision tree, a Q&A-pair device — matching whatever
`ideas/backlog.md`'s `Format`/`Angle` cells already specified for this idea.

## Cover slide hook variants

Same idea as `draft-post`'s hook-variant step, but written as the cover slide's headline (≤12
words) plus, optionally, its one-line support (≤15 words) — 2-3 different angles (direct-question,
bold-claim, plain-statement), one marked recommended.

1. ...
2. ...
3. **(recommended)** ...

## Slides

### Slide 1 — Cover
**Headline:** <the recommended hook variant above, ≤12 words>
**Body:** <one short supporting line, ≤15 words — not a paragraph>

### Slide 2 — <short label for this point>
**Headline:** <≤10 words>
**Body:** <50-90 words / 3-5 sentences, pulled from the idea's real detail>

<!-- one block per content slide — repeat to match the backlog row's real item count -->

### Slide N — Close
**Headline:** <a compact reframe or plain restatement — never an engagement-bait question, per
`voice/style-profile.md` Anti-Patterns>
**Body:** <50-90 words / 3-5 sentences, same density as a content slide>

## LinkedIn caption

<the actual post text in LinkedIn's caption box below the document — 2-4 sentences in the user's
real voice (long clause-chained sentences reformatted into short visual lines, per
`voice/style-profile.md`), hooks the reader into swiping rather than pre-summarizing every slide,
ends without an engagement-bait question, 3-5 hashtags per the current unconfirmed default.>

**Caption character count: <N>** — captions run shorter than a full text post; no fixed target
band yet (same "unconfirmed default, pending real-post feedback" caveat `draft-post` already
carries for hashtags/emoji), but tight enough to read as an invitation to swipe, not a summary
that makes swiping unnecessary.

## LinkedIn mechanics check

- Slide count matches `ideas/backlog.md`'s `Format` cell for this idea.
- Cover carries a hook line only — no paragraph.
- Every content/close slide's body is 50-90 words, sourced from real idea detail, not padding.
- No external links (caption or slides).
- En dash (–), not em dash, throughout.
- General-centric framing (no first-person "I") unless the idea's pillar is Job Search & Career
  Journey, per the Voice Framing section in `strategy/content-pillars.md`.

## Guardrail check

- No employer named or identifiable.
- No active-search mention.
- No confidential metrics.
- No coworker/manager names.
- No product/company criticism.

## Inline authenticity check (standing in for `humanize-check`)

Same checklist as `draft-post` Section 7 (anti-patterns re-check, generic AI-tell scan, chained-
sentence-rhythm confirmation, no engagement-bait close) — applied to both the slide text and the
caption, since both are published copy.
```

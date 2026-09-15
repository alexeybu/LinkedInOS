---
name: post-image
description: Generate a LinkedIn card image (PNG) for a drafted post in drafts/*.md, in the workspace's established light-card visual style. Use when the user wants an image/graphic to accompany a specific draft, or asks to regenerate/resize one.
---

# Post Image

Turns one drafted post into a single quote-card PNG in the visual style established 2026-08-24
and recolored 2026-09-11 (see note below): light ivory background, dark serif hook quote, a
large, genuinely legible topic-specific icon in a sketchy hand-drawn style, and a quiet closing
tagline. No stock photography, no gradients, no emoji-as-icon, no hustle-culture visual language —
this mirrors the same modest calibration `draft-post` applies to the text itself.

**Recolored to the light/dark carousel palette, 2026-09-11** (explicit user request — "change the
color scheme to those that is in the carousel posts"): flipped from the original deep-ink/light-text
scheme to `draft-carousel`'s light-ivory/dark-charcoal one, so a text-post card and a carousel from
the same account now read as the same visual system instead of two different ones. Exact tokens,
shared with `draft-carousel`'s `card-template.html`:
- Background: `oklch(0.965 0.012 75)` (warm ivory)
- Quote text: `oklch(0.18 0.02 50)` (near-black warm charcoal)
- Tagline text: `oklch(0.32 0.02 50 / 0.75)`
- Accent (icon strokes, rule): `#a9702c` (darkened from the old `#d9a15b` — that gold reads fine
  on deep ink but is too low-contrast on a light background; this is the same darkening
  `draft-carousel` already uses for its own accent bar/counter)
Earlier cards (drafted before this date) were rendered dark — don't regenerate them to match
unless the user asks, per this skill's standing convention for style updates.

**Icon enlarged and made a required-to-actually-work element, 2026-09-11** (same request — "add
images that fit the post," a repeat of the original 2026-08-30 ask that a 52px corner mark wasn't
fully delivering on): the earlier icon size (52px rectangular / 64px square) was small enough that
a real design (two converging lines marking a shifted constraint) rendered ambiguous — it read as
a checkmark on first look, not the shape it was meant to be. Default motif size is now **130px
rectangular / 170px square** (see the updated table in step 2) — big enough that a 2-4-element
shape stays legible after the sketchy filter's displacement, instead of collapsing into a
generic mark. Step 1's ICON guidance and step 5's QA check are both tightened to match: a small,
minimal icon (a single line or two) is no longer acceptable even if it's "clean" — build enough
real shape that the concept survives zooming out to card size.

**Kicker removed 2026-08-26** (explicit user request): earlier cards (drafted before this date)
carried an uppercase pillar-name kicker in the top-left, paired with the motif top-right. Cards
generated from this date forward drop the kicker entirely — the motif now sits alone, top-right.
Don't regenerate the earlier cards to match unless the user asks; this only governs new renders.

**Motif became topic-specific 2026-08-30** (explicit user request — "not only text, some image
related to the topic of the post"): cards through 2026-08-29 all used one fixed broken-ring motif
regardless of topic. There's no image-generation tool or stock-photo pipeline available in this
environment — see the note under step 1's ICON bullet for why a custom vector icon was the chosen
path over a real photo/AI-generated image. From this date forward, each card gets its own small
line-art icon built from the actual mechanism or claim of *that* post, in the same accent color and
stroke weight as the old ring, so the family still reads as one consistent system. Don't
regenerate earlier cards to match unless the user asks.

**Icon rendered in a sketchy hand-drawn style, 2026-09-11** (explicit user request — "add related
image in a sketchy style"): the topic icon's clean vector lines now get a hand-drawn wobble via an
SVG filter (`feTurbulence` + `feDisplacementMap`, defined once in `card-template.html` and applied
to a `<g filter="url(#sketchy)">` wrapping the icon markup) rather than rendering as perfectly
geometric paths. Same shape-per-topic logic, same accent color/stroke-width from step 1 — only the
line quality changes, from CAD-clean to sketch-clean. No new tool or library needed; this is a
pure-SVG technique that renders correctly through the existing headless-Chrome pipeline (verified
2026-09-11 via a standalone render spike). Don't hand-write the wobble into the icon's own path
coordinates — let the filter do it, so the shape logic in step 1 stays simple, clean geometry.

## 0. Identify the draft

Take the draft file path from the request. If none is given, ask which draft in `drafts/` this is
for rather than guessing.

## 1. Extract the three pieces

- **QUOTE** — the post's hook (the `## Hook` / `## Final hook` section if the draft has one,
  otherwise the opening sentence(s) of `## Full draft`). Use it verbatim, but convert straight
  quotes/apostrophes to their typographic entities (`&rsquo;`, `&ldquo;`, `&rdquo;`) to match the
  established look — don't leave straight `'`/`"` in the rendered card.
- **TAGLINE** — a short (roughly 6-12 words), plain restatement of the post's closing thought, in
  the same register as the post itself. This is a compact synthesis, not always a literal copy of
  the last sentence — the last sentence is often longer/multi-clause; distill it down the way a
  pull-quote would, without inventing a new idea the post doesn't already make. If the closing
  sentence is already short and quotable as-is, use it verbatim instead of rewording it.
- **ICON** — a single-concept line-art SVG that illustrates the post's actual mechanism or claim,
  not a generic decoration, and **big/detailed enough to actually read as that concept at render
  size**, not just abstract clutter or (worse) an accidental different shape — a 2-line icon that
  might be mistaken for a checkmark or an arrow has failed this bar, however clean the geometry is.
  Build it from simple geometric primitives (circles, lines, paths) inside a `0 0 72 72` viewBox,
  using the same accent color (`#a9702c`) and stroke-width (`3`) every time, so every card still
  reads as one visual family despite a different mark per topic. Aim for **3-5 distinct visual
  elements** (not 1-2) — enough that the shape survives both the sketchy filter's displacement and
  being viewed small in a LinkedIn feed. Draw the shape as clean, precise geometry —
  `card-template.html` applies the sketchy hand-drawn wobble automatically via its SVG filter (see
  the 2026-09-11 note above), so don't try to hand-simulate roughness in the path coordinates
  themselves. A filled accent-colored dot/shape for emphasis is fine (that's not a
  gradient or stock photography); avoid literal clipart-style objects (no calendar glyph for a
  scheduling post, no magnifying glass for an "analysis" post) — those read as generic stock-icon
  filler, which is exactly what this replaces. Think in terms of the post's actual shape: e.g. one
  filled dot connected to several open ones for a "real owner vs. several assumed ones" post, a
  tight cluster of dots with one visibly separated for a clustering/theme-check post, a single
  diverging fork for a "market sorting, not growing" post, a channel that's wide on one side and
  pinches to a marked point on the other for a "the constraint moved" post. If no clean idea with
  enough real shape to it fits the post, it's fine to keep the original broken-ring motif (given
  below as the fallback) rather than forcing a weak or under-detailed metaphor.
  - **Why a drawn icon and not a real photo/AI-generated image**: the user's initial ask was for a
    real photo or AI-generated image per post, not an abstract icon. There's no image-generation
    tool wired into this environment, and sourcing real photos would mean either the user supplying
    one per draft or this skill downloading a stock photo from the web each time (which needs
    per-file explicit permission — filename, source, size — and raises licensing questions this
    skill isn't set up to track). The user chose the drawn-icon fallback explicitly
    (2026-08-30) specifically to avoid that manual-sourcing overhead and keep the pipeline fully
    automated. If a real image ever becomes feasible (an image-gen tool gets added, or the user
    wants to hand-supply images per draft), revisit this — the current approach is a deliberate
    compromise, not a rejection of the original request.
  - **Fallback shape** (use verbatim if nothing post-specific fits):
    `<circle cx="36" cy="36" r="28" stroke="#a9702c" stroke-width="3" stroke-dasharray="150 26" transform="rotate(-90 36 36)"/>`

Don't invent content beyond what the draft already says — if the hook or close isn't a good fit
for a short card, say so rather than paraphrasing something the post doesn't actually claim. The
icon should visually match a claim/mechanism the post actually makes, not add a new idea.

## 2. Pick dimensions

**Default: rectangular, 1080×608** (established 2026-08-24 as the standing default — tighter
vertical spacing than the original square version, not a smaller type scale). Use these values in
step 3 unless asked for a different shape:

| Placeholder | Rectangular default | Square (only if explicitly requested) |
|---|---|---|
| `__WIDTH__` / `__HEIGHT__` | 1080 / 608 | 1080 / 1080 |
| `__PAD_V__` / `__PAD_H__` | 64 / 72 | 88 / 88 |
| `__MOTIF_SIZE__` | **130** (was 52 before 2026-09-11) | **170** (was 64) |
| `__QUOTE_SIZE__` | 50 (see note below) | 60 |
| `__QUOTE_MAX_WIDTH__` | 920 | 900 |
| `__TAGLINE_SIZE__` | 16 | 17 |

`__MOTIF_SIZE__` sizes the icon's rendered box only — the icon's own viewBox stays `0 0 72 72`
regardless of shape (a separate token, `__TOPIC_ICON__`, carries the actual per-post SVG markup
from step 1's ICON — see step 3).

**`__QUOTE_SIZE__` note**: 50/60 are starting points, not fixed values — a long hook in the
shorter rectangular canvas can overflow or crowd the tagline. After rendering (step 4), open the
PNG and actually look at it: if the quote block looks cramped or crowds the bottom row, drop
`__QUOTE_SIZE__` a few px (rectangular rarely needs to go below ~44px for a hook of normal length)
and re-render rather than shipping a cramped card.

## 3. Fill the template

Copy `card-template.html` (in this skill's directory) to a working file and replace every
`__PLACEHOLDER__` token with its value from steps 1-2 (a simple find-and-replace per token — sed,
or any string substitution — works fine; there's no build step). `__TOPIC_ICON__` gets the raw SVG
markup for the icon designed in step 1 (or the fallback ring shape) — it's inserted as the inner
content of the template's `<svg>` element, not escaped/wrapped as text. Keep the template file
itself untouched; always work from a fresh copy.

## 4. Render to PNG

Use headless Chrome (fall back to Edge if Chrome isn't present — check both of these before
picking one):
- `C:\Program Files\Google\Chrome\Application\chrome.exe`
- `C:\Program Files (x86)\Microsoft\Edge\Application\msedge.exe`

```bash
"<browser path>" --headless=new --no-sandbox --disable-gpu --hide-scrollbars \
  --window-size=<WIDTH>,<HEIGHT> --virtual-time-budget=4000 \
  --screenshot="<ABSOLUTE output .png path>" \
  "file:///<ABSOLUTE path to the filled working HTML file>"
```

Two things that silently break this, learned the hard way — both are non-negotiable:
- **The `--screenshot` output path must be absolute**, not relative to the current directory — a
  relative path can fail with a bare `Access is denied` and no other clue.
- **`--no-sandbox` is required** in this environment — without it, the same `Access is denied`
  failure mode shows up even with an absolute path.

`--virtual-time-budget=4000` gives the Google Fonts stylesheet time to load before the screenshot
fires — don't drop it, the card will render in fallback fonts otherwise.

## 5. Save and check

- Save the PNG into `drafts/images/<same-slug-as-the-draft>.png` in the project (create
  `drafts/images/` if it doesn't exist yet) — not only in a temp/scratch location, so it persists
  across sessions like the draft itself does.
- Read the rendered PNG back before sending it — confirm the quote isn't clipped or crowding the
  tagline, the icon rendered as the intended shape and **is actually identifiable as that concept
  at its rendered size**, not a broken-image box, not abstract clutter, and not readable as some
  *other* shape by accident (a too-simple icon collapsing into a checkmark or arrow is a fail, not
  a pass) — and confirm the fonts loaded (serif quote vs. a generic fallback is visible at a
  glance) and the light background/dark text contrast looks right. Fix and re-render if not.
- Add an `image:` field to the draft's frontmatter pointing at the saved PNG path, so the pairing
  is discoverable later.
- Send the PNG to the user.

## Ground rules

- Never invent hook/tagline text beyond what the draft actually says — this skill packages
  existing copy visually, it doesn't write new copy. The icon follows the same rule: it should
  visualize a claim/mechanism the post already makes, not introduce a new one.
- Keep the visual system consistent across cards (same colors, fonts, layout logic, line-art
  style/stroke-weight for the icon) unless the user explicitly asks for a style change —
  consistency across a series of post images matters more than novelty per card. The icon's
  *shape* is meant to vary per topic (that's the point, as of 2026-08-30); its color, stroke
  weight, viewBox size, and rendered size (130px rectangular / 170px square as of 2026-09-11)
  should not.
- The icon isn't decoration that's allowed to be an afterthought — it needs to actually be
  identifiable as the concept it represents once rendered. If a design doesn't clearly survive
  being rendered at real card size, redesign it (more elements, a clearer shape) rather than
  shipping something ambiguous just because the geometry was clean in the abstract.
- No stock photography, no gradients, no emoji-as-icon, no literal clipart-style objects (calendar
  glyphs, magnifying glasses, lightbulbs) — matches the modest, no-hype calibration already
  established for the post text itself in `draft-post`. The icon is abstract line-art built from
  the post's own mechanism, not decorative iconography bolted on afterward.

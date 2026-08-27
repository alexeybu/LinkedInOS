---
name: post-image
description: Generate a LinkedIn card image (PNG) for a drafted post in drafts/*.md, in the workspace's established dark-card visual style. Use when the user wants an image/graphic to accompany a specific draft, or asks to regenerate/resize one.
---

# Post Image

Turns one drafted post into a single dark quote-card PNG in the visual style established
2026-08-24: deep ink background, a serif hook quote, a small broken-ring "gap" motif, and a quiet
closing tagline. No stock photography, no gradients, no emoji-as-icon, no hustle-culture visual
language — this mirrors the same modest calibration `draft-post` applies to the text itself.

**Kicker removed 2026-08-26** (explicit user request): earlier cards (drafted before this date)
carried an uppercase pillar-name kicker in the top-left, paired with the motif top-right. Cards
generated from this date forward drop the kicker entirely — the motif now sits alone, top-right.
Don't regenerate the earlier cards to match unless the user asks; this only governs new renders.

## 0. Identify the draft

Take the draft file path from the request. If none is given, ask which draft in `drafts/` this is
for rather than guessing.

## 1. Extract the two pieces of text

- **QUOTE** — the post's hook (the `## Hook` / `## Final hook` section if the draft has one,
  otherwise the opening sentence(s) of `## Full draft`). Use it verbatim, but convert straight
  quotes/apostrophes to their typographic entities (`&rsquo;`, `&ldquo;`, `&rdquo;`) to match the
  established look — don't leave straight `'`/`"` in the rendered card.
- **TAGLINE** — a short (roughly 6-12 words), plain restatement of the post's closing thought, in
  the same register as the post itself. This is a compact synthesis, not always a literal copy of
  the last sentence — the last sentence is often longer/multi-clause; distill it down the way a
  pull-quote would, without inventing a new idea the post doesn't already make. If the closing
  sentence is already short and quotable as-is, use it verbatim instead of rewording it.

Don't invent content beyond what the draft already says — if the hook or close isn't a good fit
for a short card, say so rather than paraphrasing something the post doesn't actually claim.

## 2. Pick dimensions

**Default: rectangular, 1080×608** (established 2026-08-24 as the standing default — tighter
vertical spacing than the original square version, not a smaller type scale). Use these values in
step 3 unless asked for a different shape:

| Placeholder | Rectangular default | Square (only if explicitly requested) |
|---|---|---|
| `__WIDTH__` / `__HEIGHT__` | 1080 / 608 | 1080 / 1080 |
| `__PAD_V__` / `__PAD_H__` | 64 / 72 | 88 / 88 |
| `__MOTIF_SIZE__` | 52 | 64 |
| `__QUOTE_SIZE__` | 50 (see note below) | 60 |
| `__QUOTE_MAX_WIDTH__` | 920 | 900 |
| `__TAGLINE_SIZE__` | 16 | 17 |

**`__QUOTE_SIZE__` note**: 50/60 are starting points, not fixed values — a long hook in the
shorter rectangular canvas can overflow or crowd the tagline. After rendering (step 4), open the
PNG and actually look at it: if the quote block looks cramped or crowds the bottom row, drop
`__QUOTE_SIZE__` a few px (rectangular rarely needs to go below ~44px for a hook of normal length)
and re-render rather than shipping a cramped card.

## 3. Fill the template

Copy `card-template.html` (in this skill's directory) to a working file and replace every
`__PLACEHOLDER__` token with its value from steps 1-2 (a simple find-and-replace per token — sed,
or any string substitution — works fine; there's no build step). Keep the template file itself
untouched; always work from a fresh copy.

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
  tagline, the motif rendered (not a broken-image box), and the fonts loaded (serif quote vs. a
  generic fallback is visible at a glance). Fix and re-render if not.
- Add an `image:` field to the draft's frontmatter pointing at the saved PNG path, so the pairing
  is discoverable later.
- Send the PNG to the user.

## Ground rules

- Never invent hook/tagline text beyond what the draft actually says — this skill packages
  existing copy visually, it doesn't write new copy.
- Keep the visual system consistent across cards (same colors, fonts, motif, layout logic) unless
  the user explicitly asks for a style change — consistency across a series of post images matters
  more than novelty per card.
- No stock photography, no gradients, no emoji-as-icon — matches the modest, no-hype calibration
  already established for the post text itself in `draft-post`.

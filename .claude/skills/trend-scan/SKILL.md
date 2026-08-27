---
name: trend-scan
description: Research current LinkedIn content trends via web search — what formats/hooks are working, what topics adjacent to the user's pillars are getting traction, and gaps in the current pillar list — and write findings to strategy/trend-notes.md for idea-mine to build on. Use when the trend notes are stale (re-run periodically, e.g. monthly/quarterly) or the user explicitly asks for a trends refresh.
---

# Trend Scan

Feeds `idea-mine` with an external-trend layer on top of the user's own material (market research,
CV, live conversation). Answers: what's actually working on LinkedIn right now, format- and
topic-wise, and is there anything adjacent to the user's pillars that's trending but not covered?

There's no public LinkedIn API and no reliable way to pull real engagement data for arbitrary
creators — an Ahrefs social-media integration exists in this environment but it only covers
accounts the user has personally connected for scheduling/analytics (and is gated behind a plan
tier the user doesn't currently have), not competitive research. This skill works entirely from
open web research (industry write-ups, algorithm-change analyses, named-creator pattern
discussions) via `WebSearch`/`WebFetch` — treat findings as directional secondary-source
consensus, not hard data, and say so in the output.

## 0. Check current state

Read `strategy/trend-notes.md` if it exists — check its date. If it's recent (say, under ~2
months old), tell the user and ask whether to refresh anyway or skip. Trends move fast enough that
older notes should generally be refreshed, not silently reused.

## 1. Load context

Read `strategy/content-pillars.md` for the current pillars/audience so the research stays
targeted rather than generic "LinkedIn tips."

## 2. Research

Run targeted `WebSearch` queries (adjust wording/year at run time) covering:
- **Format/algorithm trends**: what post formats/structures LinkedIn's algorithm and recent
  creator advice suggest are working now (text-only vs. carousel/PDF vs. native video, ideal
  length, hook conventions, dwell-time signals, comment-bait vs. genuine discussion).
- **Topic trends in the user's specific space(s)**, derived from whatever pillars/field are
  actually in `strategy/content-pillars.md` (this may be product management, engineering,
  marketing, sales, design, or anything else — read the pillars, don't assume) — not generic
  "LinkedIn growth hacking."
- **Named creators/accounts** working in that same space, and what pattern (not literal content)
  makes their posts land — structure, angle, consistency, not word-for-word copying.
- **Gap-hunting — run this as its own deliberate search pass, not just a byproduct of the other
  three.** Actively search for topics trending in spaces adjacent to the user's pillars/field
  (adjacent disciplines, tooling debates, market/process trends the user's audience would care
  about) that aren't represented in any current pillar. Don't just note what happened to come up
  incidentally — spend real queries on this specifically, the same way you'd research the pillars
  themselves. For each candidate found, do a quick "does this actually add something the pillars
  don't already cover" check before including it.

Use `WebFetch` on a handful of the most relevant results for more detail where a search snippet
isn't enough. Prefer recent sources (last 6-12 months) given how fast platform dynamics shift.

## 3. Write findings

Write `strategy/trend-notes.md` with a `last_updated` date and these sections:
- **Format Trends**
- **Topic Trends** (organized by existing pillar, so it's easy for `idea-mine` to map to one) —
  for each pillar, prefer a genuine analytical take (which side of a live debate is more
  defensible, and why, especially where it connects to something specific and real the user has
  already said or done) over a flat summary of what sources report.
- **Notable Creators/Patterns** (name + the pattern, not their text)
- **Gap Candidates — Declined**: topics already considered and explicitly passed on during a past
  `content-strategy` run (check `strategy/content-pillars.md` for anything that reads like a
  deliberate omission) — flag so they don't get silently re-proposed.
- **Worth Exploring — New, Outside Current Pillars, Occasional Only**: the actual output of the
  dedicated gap-hunting pass above. These are not proposals for a new pillar — frame each as an
  occasional, one-off angle, with a one-line note on why it's worth it and how it could connect to
  the user's own real material. Never fold these into the pillar list yourself.

Do not quote any single source for more than ~15 words, and never reproduce a creator's post text
at length — synthesize the pattern in your own words and cite/link the source.

## 4. Confirm

Summarize the headline findings and gap candidates for the user, and ask whether any gap should
become a new pillar (→ re-run `content-strategy`) or just inform occasional posts within existing
pillars.

## Ground rules

- Findings are directional secondary-source consensus, not verified data — say so, don't overstate
  confidence.
- Never fold a "gap candidate" topic into the pillar list yourself — that's a `content-strategy`
  decision the user makes explicitly.
- Respect copyright: synthesize patterns, don't reproduce creators' post text at length.

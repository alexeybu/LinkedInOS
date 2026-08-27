---
name: idea-mine
description: Mine real material into a tagged backlog of concrete LinkedIn post ideas in ideas/backlog.md, filtered through strategy/content-pillars.md and its guardrails. Use when the idea backlog is running low, or when the user wants fresh post concepts.
---

# Idea Mine

Turns real material — not generic "content ideas" — into a pillar-tagged backlog of specific post
concepts. Every idea here should trace to something real: a market-research finding, a real
(anonymized) accomplishment, or something the user actually said. `draft-post` picks one entry from
here and turns it into an actual post.

## 0. Check current state

Read `ideas/backlog.md`. If it already has un-drafted entries, ask whether this run should add
more (and how many, roughly, given the cadence in `strategy/content-pillars.md`), refresh/re-tag
stale ones, or be skipped.

## 1. Load constraints first

Read `strategy/content-pillars.md` (pillars + audience + **guardrails** — binding, not optional)
and `voice/style-profile.md` (structural patterns: this user favors direct-question opens,
skeptical-then-credit argument shape, analogy-driven closes, inline-dash lists over bullets — bias
idea *angles* toward shapes that'll actually draft well in this voice, not generic hooks).

## 2. Mine real sources

LinkedInOS is a standalone skillset — don't reach into sibling projects (JobOS or otherwise) or
assume any particular local file layout exists. Real material comes from memory and from the user
directly:

- **Memory** — check for anything already surfaced from a prior session (real accomplishments,
  market/industry findings, career history) that's relevant to a pillar. Use it the same way a
  cited source would be used, and note in the idea's Source column that it came from memory.
- **Live conversation** — ask the user (open chat, not a rigid form) for real material per pillar:
  a market/industry finding they've seen recently, a real accomplishment or metric from their work
  (to be anonymized per guardrails — draft the idea already framed generically, e.g. "a company I
  worked at," never carrying a real employer name into `ideas/backlog.md`), or anything recent — a
  decision, a debate, an opinion, something that annoyed or surprised them at work. This is usually
  the richest source; one or two good prompts per pillar tend to surface something usable.
- If the user has files they want mined (a CV, research notes, anything else), ask them to paste
  the relevant content or point you to the specific path explicitly for this run — don't assume a
  default location.

Don't force every source on every run — use what's productive, and don't manufacture an idea that
isn't backed by something real just to hit a round number.

## 3. Shape each idea

For each candidate, write:
- **One-line concept** — specific enough that `draft-post` doesn't have to invent the substance.
- **Pillar** tag (must match one of the pillars actually defined in `strategy/content-pillars.md`).
- **Angle/hook shape** — reference the voice profile's preferred shapes where it fits (e.g.
  "skeptical-first, credit-second" or "direct-question open") rather than leaving it generic.
- **Source** — one line on where this came from (a research finding, a CV accomplishment
  anonymized, something said live) so `draft-post` can go back to it for real detail.
- **Guardrail check** — a quick explicit note that it doesn't name a real employer, doesn't reveal
  applied-to companies, doesn't include confidential metrics, and doesn't criticize a named company
  (or, for product teardowns, critiques the product/decision rather than attacking the company).

## 4. Write the backlog

Write/append to `ideas/backlog.md` as a table (columns: Pillar, Concept, Angle, Source, Status —
`Status` starts as `new`). Aim for rough pillar balance rather than clustering — check the existing
backlog's pillar distribution before adding more of one and not others.

## 5. Confirm

Show the user the new entries (or a summary if there are many) and ask if any should be cut,
reworded, or re-tagged before finalizing.

## Ground rules

- Every idea must trace to something real — a cited finding, a real (anonymized) accomplishment,
  or something the user actually said in conversation. No invented anecdotes or fabricated stats.
- Guardrails from `strategy/content-pillars.md` are binding here, not just at draft time — don't
  backlog an idea that would require breaking one (e.g. an idea that only works if a company is
  named).
- This skill proposes concepts and angles, not finished copy — leave the actual writing to
  `draft-post`.

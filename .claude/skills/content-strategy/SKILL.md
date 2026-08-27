---
name: content-strategy
description: Define or update strategy/content-pillars.md — content pillars, target audience, goals, cadence, and off-limits topics for LinkedIn posting. Use when setting up or revising the LinkedIn content strategy itself (what to post about, who it's for, how often, what "working" means), as opposed to drafting an individual post.
---

# Content Strategy

Defines the strategic layer every other LinkedInOS skill reads from: what topics to post about,
who they're for, how often, what success looks like, and what's off-limits. `idea-mine` filters
ideas through the pillars here; `draft-post` and `review-performance` both check goals/audience
here too.

## Interaction style

Same as `voice-profile`: drive this with `AskUserQuestion` for anything enumerable, batching
related questions (up to 4 per call). Reserve open chat for things a widget can't hold well (e.g.
naming specific off-limits topics/employers).

## 0. Check current state and reuse what's already known

Read `strategy/content-pillars.md`. If it already has real content, ask whether this run replaces
it, updates specific sections, or is skipped.

JobOS is a separate project and may not be present on this machine or in this workspace — do not
read `../JobOS/jobs/search-profile.md` directly. Instead, check memory for anything already known
about the user's target roles, seniority, industries, or region (e.g. from a prior JobOS session
surfaced into memory). If memory has it, use it to define the recruiter/HR side of the target
audience for free — don't re-ask "who are you targeting" from scratch; instead confirm it:
summarize what memory says and ask if the LinkedIn content audience should match that exactly or
differ (e.g. a broader peer audience in the same field, in addition to recruiters at those kinds of
companies). If memory has nothing on this, ask the target-role/seniority/region questions directly
instead of assuming a field (don't default to product management or any other specific function).

## 1. Goals

Ask what success concretely looks like and over what rough timeframe — options like: more
recruiter/HR inbound (DMs, InMails), higher SSI, more profile views, growing a peer following for
its own sake, or a mix. If they have a number in mind (e.g. "SSI back above 39, ideally higher") or
a timeframe, capture it — otherwise leave it directional rather than inventing a target.

## 2. Content pillars

Propose a starting set based on what the user has already said in conversation about what they
want to post about, and confirm/refine via `AskUserQuestion` (multiSelect from suggested pillars,
plus free-text "Other"). Aim for 3-4 pillars — more than that dilutes the calendar and makes
`idea-mine` harder to balance. For each confirmed pillar, capture a one-line definition of what it
does and doesn't include (e.g. "hands-on tactics — concrete frameworks/techniques actually used,
not general career advice").

Consider whether "building LinkedInOS itself" / "using Claude Code in their work" deserves to be a
pillar or a recurring bit within another one — it's authentic, on-brand material if the user's
work involves AI tooling, but check with the user rather than assuming they want to publicize the
tool itself.

## 3. Cadence

Ask for a sustainable posts/week number — offer options like 1, 2-3, daily, or "flexible/no fixed
cadence," and note that consistency matters more than frequency for LinkedIn's algorithm and for
recruiter perception, so a lower sustainable number beats an ambitious one that lapses.

## 4. Off-limits / guardrails

This matters more than usual here because the user is actively job hunting and has real employer
history to draw on for stories (e.g. the Profitero story already in `voice/style-profile.md`).
Ask explicitly:
- Any current/former employers, clients, or ongoing negotiations that shouldn't be named or
  identifiable, even indirectly.
- Any topics off-limits entirely (e.g. specific product/company criticism, confidential metrics,
  ongoing job-search details like which companies they've applied to).
- Whether it's fine to reference the active job search itself in posts (some people post "I'm
  looking" content deliberately; others prefer it stays implicit/never mentioned).

## 5. Write the file

Write `strategy/content-pillars.md` with sections: Goals, Audience (merged JobOS target-role data
+ any LinkedIn-specific additions), Pillars (each with a one-line definition), Cadence, and
Guardrails (off-limits topics/employers/details). Keep it as concrete, checkable statements, not
vague aspirational language.

## 6. Confirm

Show the user a short summary and confirm it's right before wrapping up.

## Ground rules

- Never publish or infer strategy decisions the user didn't actually make — if goals/cadence
  weren't discussed, leave them open rather than guessing a number.
- Guardrails here are binding for every other skill (`idea-mine`, `draft-post`) — treat anything
  listed as off-limits as a hard constraint, not a style preference.

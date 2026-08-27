# Claude LinkedInOS

A [Claude Code](https://claude.com/claude-code) workspace that runs an entire LinkedIn content
pipeline as a set of skills: capture your real writing voice, define what you post about and why,
mine real work into concrete post ideas, draft posts that read as human-written, generate a card
image for each, and track what actually performs. Nothing here posts to LinkedIn automatically —
every step produces a file you review, and you publish it yourself.

This repo ships the framework (skills + folder structure) only. The content it generates for you —
your voice profile, strategy, ideas, drafts, images, performance log — is personal and is
git-ignored; it fills in locally as you run each skill. A fresh clone will show empty folders with
just a `README.md` in each until you start working through the steps below.

> This workspace can optionally pull target-role context from a sibling job-search project (via
> Claude's memory) if one happens to exist on your machine — but it works completely standalone.
> Nothing here requires any other project to be present.

## Requirements

- [Claude Code](https://claude.com/claude-code) installed and authenticated.
- Run `claude` from this directory so `.claude/skills/` is picked up.

## Step-by-step setup

Run these as slash-style requests to Claude Code inside this workspace, in order. Each step is a
skill in `.claude/skills/`; re-run any of them later to update that layer.

### 1. `voice-profile` — capture how you actually write

**Say:** "run voice-profile" (or just "set up my writing voice").

Builds `voice/style-profile.md`, the single source of truth every drafting skill reads from. Works
from real writing samples if you have them (past LinkedIn posts, emails, Slack messages you paste
in) or a short guided interview if you don't. Every trait it records has to trace back to
something you actually wrote or said — it will not invent a generic "punchy LinkedIn voice." Run
this first; re-run it whenever your voice feels like it's drifted.

### 2. `content-strategy` — decide what you post about and why

**Say:** "run content-strategy."

Builds `strategy/content-pillars.md`: your 3-4 content pillars, target audience, posting cadence,
what success looks like (SSI, profile views, reachouts), and explicit off-limits topics. Every
other skill downstream reads this file — `idea-mine` filters ideas through it, `draft-post` and
the future `review-performance` check goals/audience against it. Revisit this periodically as your
job search or focus shifts.

### 3. `trend-scan` — refresh external context (optional, periodic)

**Say:** "run trend-scan."

A web-research pass on current LinkedIn format/topic trends and named-creator patterns in your
space, plus a gap-check against your pillar list. Writes `strategy/trend-notes.md`. There's no
public LinkedIn API for real engagement data, so this is directional secondary-source research,
not hard analytics — treat it as a supplement to `idea-mine`, not a requirement. Re-run monthly or
quarterly; you don't need to run it before every `idea-mine` pass.

### 4. `idea-mine` — turn real material into post concepts

**Say:** "run idea-mine" (or "I need more post ideas").

Mines real material — memory, `strategy/trend-notes.md` if present, things you say in the live
conversation, or content you explicitly paste/point to — into pillar-tagged, concrete post
concepts in `ideas/backlog.md`. Every idea traces to something real (a real accomplishment, a real
observation, an actual finding) — never a generic "content idea." It will not source ideas from
this workspace or any sibling project itself. Run this whenever the backlog is running low.

### 5. `draft-post` — write an actual post

**Say:** "draft the [idea name] post" (or "run draft-post" to be asked which idea).

Takes one idea from `ideas/backlog.md` and writes a real post in your voice: 2-3 hook variants
plus a full draft, respecting LinkedIn's real mechanics (length, the "see more" hook cutoff, no
in-body links) and a deliberately modest, non-engagement-bait structure. Runs an inline
authenticity check against `voice/style-profile.md` before finishing. Writes
`drafts/<date>-<slug>.md`.

### 6. `post-image` — generate a card image (optional, per draft)

**Say:** "make an image for the [slug] draft."

Generates a single dark quote-card PNG for a specific draft: a serif hook quote, a small
broken-ring "gap" motif, and a quiet closing tagline — no stock photography, no gradients, no
hustle-culture visual language. Saved to `drafts/images/<date>-<slug>.png`, referenced from the
draft's frontmatter. Skip this for any post you don't want a card for.

### 7. Publish it yourself

Copy the draft (and image, if you made one) to LinkedIn and post it. This workspace never
publishes on your behalf — LinkedIn automation risks the account and isn't something Claude Code
does here regardless.

### 8. `log-performance` *(not yet built)* — record what happened

Once available, this will let you paste in stats (views, reactions, comments, profile views, SSI)
for a published post into `published/performance-log.md`.

### 9. `review-performance` *(not yet built)* — learn from what worked

Once available, this will read the performance log, report what's working by pillar/format/
hook/timing, and feed findings back into `content-strategy` and `idea-mine`.

## Other skills

- **`cleanup-strategy`** — resets `strategy/content-pillars.md`, `strategy/trend-notes.md`, and
  `ideas/backlog.md` back to empty/placeholder state, backing everything up first (to
  `_strategy-backups/`, also git-ignored). Never touches `voice/style-profile.md`. Use this to
  re-run steps 2-4 cleanly, e.g. after testing or a genuine strategy reset.

## Layout

See [CLAUDE.md](CLAUDE.md) for the full folder-by-folder layout, the skill list with build status,
and the workspace's ground rules (no fabricated content, no auto-posting, voice profile stays
evidence-based).

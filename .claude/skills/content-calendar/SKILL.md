---
name: content-calendar
description: Maintain strategy/calendar.md — the posting schedule, pillar-rotation order, and the week-by-week mapping of drafted/backlog posts onto calendar slots. Use when the user wants to schedule what goes out when, map new drafts or backlog ideas onto specific dates, or refresh the calendar after a post goes out.
---

# Content Calendar

Maintains `strategy/calendar.md`: the recurring weekly schedule (days/times/cadence), the pillar
rotation order, and a log table mapping specific drafts or backlog ideas onto actual calendar
dates. Doesn't publish anything — LinkedInOS never posts on the user's behalf; this only tells
them what to post when, and tracks status (`needs draft-post` → `ready to post` → `posted`) as
drafts get written and posts actually go out.

## 0. Check current state

Read `strategy/calendar.md` if it exists. If it already has a weekly schedule and pillar rotation,
reuse them — don't re-derive the schedule from scratch, or ask about it again, unless the user
wants to change cadence/days/times. If the file doesn't exist yet, this is a first run: build the
schedule (step 1) before mapping anything (step 2).

## 1. Establish the weekly schedule (first run, or on explicit request)

Read `strategy/content-pillars.md` for cadence (posts/week) and pillar balance (primary rotation
vs. lower-priority pillars). Use `AskUserQuestion` (batched) for anything not already decided:
posting days, a primary time slot, and — if cadence allows a 3rd weekly post — a secondary slot.

Default reasoning when the user has no preference: mid-week days (Tue/Wed/Thu) over Monday
(inbox/catch-up) or Friday/weekend (engagement drop-off) for a B2B/recruiter audience; a morning
commute window or a midday lull over evenings. State the reasoning inline in the file, not just
the conclusion, so a future run (or the user) can see *why* a slot was picked and revisit it once
`published/performance-log.md` has real engagement data to replace the default with.

Write into `strategy/calendar.md`:
- **Posting Schedule** — basis (best-practice default vs. personalized once performance data
  exists), cadence, days, times, and a weekly-template table.
- **Pillar Rotation** — the round-robin order across primary pillars, plus where/how often the
  lower-priority pillar(s) drop in. Match the ratio in `strategy/content-pillars.md`'s Cadence
  section (e.g. "roughly 1 in 5 slots") — don't hardcode a fixed weekly day for a pillar the
  strategy says should be occasional, not scheduled.

## 2. Map posts onto the schedule

This is the part that runs most often: mapping what's actually available (drafted or backlog-only)
onto upcoming calendar slots.

- Read `ideas/backlog.md` for status (`new`, or `drafted → <path>`) and `drafts/` for what's
  actually been written.
- Walk the pillar rotation forward from the last logged slot (or from today if there's no prior
  log), assigning the next unposted item for that slot's pillar. Prefer already-drafted posts over
  backlog-only ideas for the nearest upcoming slots — an idea that hasn't been drafted yet can't
  realistically be posted on schedule.
- For each slot, record: date, pillar, the specific draft or backlog concept (linked via relative
  path when a draft file exists), and status:
  - `needs draft-post` — backlog idea only, no draft yet.
  - `ready to post` — drafted, not yet confirmed published.
  - `posted` — **only** when the user explicitly confirms it went out. Never infer this from the
    slot's date having passed — LinkedIn has no API to check, so the user's word is the only
    source of truth.
- If a pillar's queue is thin (fewer than ~2 upcoming slots' worth of drafted-or-backlog material),
  flag it as a gap rather than filling it — that's a signal to run `idea-mine` or `draft-post` for
  that pillar, not something this skill generates itself.

## 3. Reconcile drift before adding new slots

Check whether anything already logged has changed status since the last run:
- A backlog entry that's since been drafted — update `needs draft-post` → `ready to post` with the
  new draft path.
- A post the user mentions went out on a different day than planned — correct the date in place
  and add a short dated correction note (matching the existing log's "Correction (date): ..."
  style) rather than silently rewriting history.

## 4. Write the log

Append/update the log table in `strategy/calendar.md` (columns: Date, Pillar, Draft/Concept,
Status). Add a short prose note above the table whenever this run's mapping logic deviated from
the default rotation (e.g. compressing the cycle onto a 3rd weekly slot because enough material
was ready) — the file's existing log entries are the model for this. Update the `last_updated`
frontmatter field.

## 5. Confirm

Show the user the updated/new slots and ask if the order, dates, or pillar assignment need
adjusting before finalizing — especially if step 3 moved or corrected anything.

## Ground rules

- Never mark anything `posted` without the user explicitly confirming it — no inferring from the
  calendar date having passed.
- Never invent a draft or backlog idea to fill a thin slot — flag the gap and point to
  `idea-mine`/`draft-post` instead.
- Respect the pillar-balance ratio from `strategy/content-pillars.md`; don't let convenience (e.g.
  "this pillar has more ready drafts") silently override the intended rotation — flag it if it did.
- This skill schedules and tracks. It never posts anything itself.

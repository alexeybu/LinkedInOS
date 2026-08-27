---
name: cleanup-strategy
description: Reset the outputs of content-strategy, trend-scan, and idea-mine back to placeholder/empty state, backing everything up first. Use when the user asks to clean up, reset, wipe, or start over with the content strategy / trend notes / idea backlog (as opposed to the voice profile, which this never touches).
---

# Cleanup Strategy

Resets the parts of this workspace that `content-strategy`, `trend-scan`, and `idea-mine` fill in,
back to placeholder/empty state — for re-running those skills cleanly during validation/testing,
or a genuine strategy reset. Always archives before touching anything live. Never touches
`voice/style-profile.md` — that's a separate, earlier-validated piece.

## Scope

Resets:
- `strategy/content-pillars.md` — deleted (the `strategy/README.md` placeholder stays as-is)
- `strategy/trend-notes.md` — deleted
- `ideas/backlog.md` — deleted (the `ideas/README.md` placeholder stays as-is)

Does **not** touch:
- `voice/style-profile.md`
- `strategy/calendar.md` (the `content-calendar` skill's own output, out of scope here)
- `drafts/`, `published/`, `templates/`

## 1. Show current state and confirm scope

Before touching anything, check which of the three files actually exist and have real content.
Show the user a concrete summary (e.g. "content-pillars.md has your 4 pillars + guardrails,
trend-notes.md has a trend pass from <date>, backlog.md has N ideas") rather than a generic
warning.

Ask via `AskUserQuestion` which of the three to actually reset this run (defaulting to all three,
but letting the user narrow it — e.g. "just wipe the backlog, keep my pillars"). **Do not proceed
until they confirm.** This runs every time, even if invoked with "just clean it up, don't ask."

## 2. Archive first

Create a timestamped backup directory: `_strategy-backups/<yyyy-mm-dd-HHMMSS>/`, mirroring the
source paths (e.g. `.../strategy/content-pillars.md`). Copy every file about to be deleted into it
first. Skip a file entirely if it doesn't exist or has no real content.

## 3. Reset the confirmed scope

Delete each confirmed file. Leave the corresponding folder's `README.md` placeholder untouched.

## 4. Confirm

Show what was backed up (the `_strategy-backups/<timestamp>/` path) and what was reset. Remind the
user that `content-strategy` is the natural next step to repopulate the pillars.

## Ground rules

- Never skip the confirm step, regardless of phrasing.
- Always back up before deleting — no exceptions, even for one file.
- Never touch `voice/style-profile.md`, `templates/`, `drafts/`, or `published/` regardless of the
  confirmed scope.
- If a backup copy fails for any file, stop and tell the user rather than deleting the original.

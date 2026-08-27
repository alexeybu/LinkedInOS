---
name: draft-post
description: Take one idea from ideas/backlog.md and turn it into a polished, voice-matched LinkedIn post draft in drafts/<date>-<slug>.md, with 2-3 hook variants, LinkedIn mechanics respected, and an inline authenticity check. Use when the user wants to draft an actual post, as opposed to generating ideas or setting strategy.
---

# Draft Post

Takes one real idea and writes an actual LinkedIn post in this user's voice — not a generic
"content template" filled in with their name. Every draft here should read like something they'd
actually post, survive a genuine gut-check against `voice/style-profile.md`, and respect LinkedIn's
real mechanics (length, hook cutoff, formatting) without chasing engagement-bait tactics.

## Interaction style

Same as the other LinkedInOS skills: batch enumerable choices with `AskUserQuestion`, use open
chat for anything that needs real judgment (picking between close variants, reacting to a full
draft). If the user already named which idea to draft (in this message or earlier in the
conversation), skip the picking step and confirm the concept in one line before proceeding.

## 0. Pick the idea

If the user pointed at a specific idea (by description or by row), use that one — restate it in
one line to confirm you've got the right row before writing anything.

Otherwise, read `ideas/backlog.md`, filter to `Status: new`, and either recommend one (with a
one-line reason tied to the pillar balance, the Content Type Preference, or how strong the
underlying source material is) or ask the user to pick via `AskUserQuestion` if there's no clear
standout.

Once chosen, update that row's `Status` to `drafting` in `ideas/backlog.md`.

## 1. Load constraints

Read, in this order:
- **`voice/style-profile.md`** — tone, rhythm, structural patterns (the take/op-ed vs.
  narrative/lesson-learned templates), vocabulary quirks, formatting habits, anti-patterns. This
  is the single source of truth for what this user's voice actually sounds like — don't invent
  traits it doesn't already document.
- **`strategy/content-pillars.md`** — confirm the idea's pillar, re-read the **guardrails**
  (binding, not optional: anonymize companies, never mention the active search, no
  product/company criticism, no confidential metrics, no coworker names) and the **Content Type
  Preference** (default to practical/knowledge-sharing payload over stat-led trend commentary,
  per the 2026-08-24 addition — a stat can open a post, but the payload should teach something
  usable).
- **`strategy/trend-notes.md`**, if present — format-trend mechanics (see LinkedIn Mechanics
  below) and any pillar-specific angle notes relevant to this idea.
- The chosen row in **`ideas/backlog.md`** — concept, angle, source, guardrail check. Go back to
  the cited source material for real specifics rather than inventing detail the idea note doesn't
  already contain.

## 2. LinkedIn mechanics (hard constraints)

- **Hard ceiling: never exceed LinkedIn's ~3,000-character post limit.** This is a platform limit,
  not a style choice — check the final draft's character count explicitly before finishing.
- **Target length: roughly 900-1,400 characters**, per `voice/style-profile.md`'s existing
  guidance and the format-trend research in `strategy/trend-notes.md` (posts that get fully read
  reportedly out-signal longer posts that get abandoned partway). This is a target band, not a
  hard rule — let the actual content decide, but treat going well outside it as a reason to
  reconsider, not a reason to pad.
- **The hook must land inside ~140 characters** (the mobile truncation point before "see more") —
  it has to make sense and create a reason to click on its own, not depend on what comes after the
  cutoff.
- **No external links in the post body** — reportedly suppresses reach 40-50%. If a link is
  genuinely needed, note it for the first comment instead, never inline.
- **Reformat the user's long clause-chained sentences into short visual lines** (line breaks
  between clauses) rather than shortening the sentences themselves — per `voice/style-profile.md`'s
  explicit instruction to `draft-post`. Don't flatten the voice to fit the medium.
- **Formatting habits**: inline-dash lists over bullet lists (per the confirmed pattern in
  `voice/style-profile.md`); light emoji use and 3-5 hashtags as the current *unconfirmed default*
  (flag this in the draft's notes as still needing real-post feedback to confirm, per that file's
  own Gaps section) — don't invent heavier formatting than that default.

## 3. Calibrate: proven structure, dialed-down intensity

Draw on what actually works on LinkedIn (a real, specific hook; one clear idea per post; a
structure that holds attention rather than front-loading everything) — but **deliberately dial
down the pushy/hyped register that "viral" LinkedIn advice usually implies.** Concretely:

- No manufactured urgency, no "this will change how you think about X forever" superlatives, no
  engagement-bait CTA endings ("What do you think? 👇") — these are already ruled out by
  `voice/style-profile.md`'s Anti-Patterns, and this instruction doesn't loosen that, it reinforces
  it.
- Prefer a **modest, confident-but-not-declarative** register — state the point plainly and let
  the substance carry it, rather than oversell it. If a sentence reads like it's trying hard to
  sound impressive, cut the trying-hard part and keep the substance.
- This calibration is a drafting instruction, not a discovered voice trait — don't write it into
  `voice/style-profile.md` itself. It governs *how this skill drafts*, applied on top of whatever
  the style profile already documents as genuinely this user's voice.

## 4. Pick the structural template

Match the idea to one of the shapes `voice/style-profile.md` documents:

- **Take/op-ed** (excitement-first, brief caution mid-post, resolves via a real thesis or compact
  reframe) — for opinion/analysis-flavored ideas.
- **Narrative/lesson-learned** (chronological, plain unhedged consequence, short imperative-list
  close) — for personal-story-flavored ideas (mainly the Job Search & Career Journey pillar).
- **Practical/how-to** (a shape not yet validated by a real sample, used for the Content Type
  Preference's practical ideas): open on why it matters in one or two lines, deliver the actual
  process/framework/checklist as the payload, close with a plain, confident restatement rather
  than an engagement question. **Flag in the draft's notes that this template is inferred, not
  yet evidence-backed** — it should get folded into `voice/style-profile.md` properly once a few
  real how-to drafts/posts exist to confirm the shape, per that file's own evidence-driven ground
  rules.

## 5. Write 2-3 hook variants

Each variant: a different open style (e.g. direct-question, bold-claim, plain-statement), each
self-contained within the ~140-character cutoff, each consistent with the chosen template. Note
which one you'd lead with and why, but leave the actual choice open for the user to react to.

## 6. Write the full draft

Using the recommended hook, write the complete post: the payload (the real substance — the
process, the take, the story), the close, formatting per Section 2. Anonymize per guardrails as
you go — don't write a real employer name and plan to fix it later.

## 7. Inline authenticity check

`humanize-check` doesn't exist as a standalone skill yet — until it does, run this check inline
before finalizing:

- Re-read against `voice/style-profile.md`'s Anti-Patterns list directly — does anything here read
  like the hype/hustle/fake-vulnerability/humble-brag patterns it explicitly rules out?
- Scan for generic AI writing tells: throat-clearing opens ("In today's fast-paced world..."),
  "Let's dive in," em-dash-as-crutch overuse beyond what's actually documented as this user's
  pattern, empty intensifiers ("game-changer," "unlock," "leverage" as a verb), triplet-parallelism
  padding ("It's not just X, it's Y, it's Z"), and generic listicle-emoji section headers.
- Confirm the long-clause rhythm actually survived reformatting into short lines — re-flatten the
  draft mentally and check it still reads as one of the user's real, chained sentences, not a
  series of short choppy fragments that only look like their voice at a glance.
- Report what you checked and found, even if the answer is "nothing flagged" — don't silently fix
  and move on without saying what changed. This step should be easy to extract into a real
  `humanize-check` skill later; keep its logic self-contained here for that reason.

## 8. Save and update state

- Write `drafts/<date>-<slug>.md` containing: the source idea reference, the 2-3 hook variants
  (with the recommended one marked), the full draft, its character count, a one-line guardrail
  confirmation, and the structural-template note from Section 4.
- Update the idea's row in `ideas/backlog.md` from `drafting` to `drafted`.

## 9. Confirm

Show the user the full draft (hook variants + body + character count) and ask for real reaction —
cut, reword, re-hook, or approve. This workspace never posts on the user's behalf (see root
`CLAUDE.md`) — the deliverable is the drafted file, posting is always manual.

## Ground rules

- Never fabricate detail beyond what the source idea/material actually supports — go back to the
  cited source rather than inventing specifics to make a post feel more concrete.
- Guardrails in `strategy/content-pillars.md` are binding here, not a style preference — an idea
  that would require breaking one should be flagged back to the user, not quietly drafted around.
- Never exceed LinkedIn's real character limit, and never post/publish on the user's behalf.
- This skill writes drafts, not final copy carved in stone — expect and invite edits.

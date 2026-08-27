---
name: voice-profile
description: Build or update voice/style-profile.md, the writing-voice source of truth for every other LinkedInOS drafting skill. Works from real writing samples if the user has them, or a short interview if not. Use when the user asks to set up, capture, build, or update their writing voice/style profile, or when a drafting skill would need one that doesn't exist yet.
---

# Voice Profile

Builds `voice/style-profile.md` — the single source of truth every drafting/humanize skill in this
workspace reads from. The whole point of this workspace is posts that sound like the user, not
like an AI wrote them, so this skill is intentionally evidence-driven: every trait it records
should trace back to something the user actually wrote or actually said, never a generic guess at
"good LinkedIn voice."

## Interaction style

Drive this with the `AskUserQuestion` tool for anything with enumerable options (source type,
tone dimensions, etc.), same as JobOS's `setup` skill. Fall back to open chat only where a widget
genuinely can't hold the answer — e.g. asking the user to paste actual post text.

## 0. Check current state first

Read `voice/style-profile.md`. If it already has real content (not a placeholder), tell the user
what's there and ask whether this run should replace it entirely, refine specific sections, or add
more samples on top of the existing profile — don't silently overwrite a working profile.

## 1. Establish the source material

Ask (via `AskUserQuestion`) how they want to provide material to learn from. Offer:

- **Paste past LinkedIn posts** — the ideal source, since it's the exact target medium.
- **Point to files/a folder** — e.g. a LinkedIn data export, saved posts doc, or any folder of
  past posts.
- **Other writing samples** — emails, Slack messages, docs, cover letters — useful if they have
  no saved LinkedIn history; note in the profile that these are a proxy, not the target medium,
  and flag that tone may need light adaptation for LinkedIn's more public register.
- **No samples — interview me instead** — go to step 2b.

Users can combine sources (e.g. a few LinkedIn posts plus some Slack messages) — don't force a
single-source choice if they offer more than one.

## 2a. Learn from samples

Collect the material (pasted text, read attached/pathed files — use the `docx`/`pdf` skills if
needed for those formats). Aim for enough volume to spot real patterns, not just one post — if the
user only offers one or two short samples, say so and suggest either finding more or supplementing
with a short interview (step 2b) to fill gaps.

Analyze for concrete, citable patterns:
- **Sentence & paragraph rhythm** — short punchy lines vs longer flowing sentences, typical post
  length, how paragraphs break (LinkedIn line-break habits).
- **Vocabulary & register** — casual vs formal, jargon they use naturally vs avoid, filler words
  or verbal tics, swearing/informality tolerance.
- **Formatting habits** — emoji use (none/rare/frequent, which ones), hashtag use, bullet/numbered
  list habits, bold/caps for emphasis, em-dash or other punctuation quirks.
- **Structural patterns** — how they open (question, bold claim, mini-story, stat), how they
  close (question to readers, CTA, no CTA at all), storytelling vs listicle vs hot-take shape.
- **Voice/personality** — humor style (dry, self-deprecating, none), first-person vulnerability
  vs authority framing, how opinionated vs hedged they are.
- **Anti-patterns** — anything conspicuously absent that a generic LinkedIn post would have (e.g.
  never uses hustle-culture phrases, never says "I'm excited to announce," no hashtag blocks).

## 2b. Interview (no samples available)

Run a short, conversational `AskUserQuestion` sequence (batch related questions, up to 4 per
call) covering the same dimensions as above at a lighter level: tone (casual/professional/blend),
emoji/hashtag comfort, sentence-length preference, humor style, first-person comfort, and 2-3
"LinkedIn voice" clichés they specifically want to avoid sounding like.

Then ask for one live sample: pick a real, small topic (e.g. "describe a recent work decision you
made and why, like you're telling a colleague") and have them write a few sentences in chat,
unedited. Analyze that raw text the same way as step 2a — a real sample beats inferred preferences
even when it's short.

## 3. Write the profile

Write `voice/style-profile.md` with clear sections: Summary (2-3 sentences), Tone & Register,
Sentence & Paragraph Rhythm, Vocabulary, Formatting Habits, Structural Patterns (opens/closes),
Anti-Patterns (what to avoid), and a short "Evidence" section listing which real samples/answers
each major trait is based on. Quote 1-2 short real phrases per section where possible rather than
paraphrasing them into generic adjectives — actual wording is more useful to future drafting than
"casual and direct."

Do not add traits that weren't backed by evidence — if a dimension is genuinely unclear from the
material provided, leave it marked `(not yet determined — needs more samples)` rather than
guessing.

## 4. Confirm

Show the user the finished profile and ask if it actually sounds like them before wrapping up —
this is the foundation every future draft depends on, so it's worth a real gut-check, not a rubber
stamp.

## Ground rules

- Every trait must trace to real evidence (a quoted sample or an explicit answer), never an
  assumption about what "good LinkedIn voice" looks like in general.
- Don't smooth the profile toward generic professional-polish language — the point is to capture
  what's distinctive, including quirks a style guide would normally "fix."
- Re-runnable any time the user's voice drifts or they get more samples to add.

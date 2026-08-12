---
name: scratch-ideas
description: >
  Has two modes. Quick mode: use when the user drops a bare capture ask — "log this
  idea", "I have an idea", "add this to ideas" — into a conversation that's otherwise
  about something else; just logs the idea in one exchange and lets the user get back to
  what they were doing, nothing else. Review mode: use when the user opens a thread
  specifically to work through their ideas — "review ideas", "what ideas am I sitting
  on", "what's been filed", "file this idea away", "promote this idea", "share this idea
  with the team", "kill this idea", "prune ideas", "what's been sitting too long" — and
  runs the full capture/review/file-away/promote/prune flow ending in a nudge. Personal
  capture lives in IDEAS.md at the scratch-pad repo root (gitignored, personal — created
  from templates/IDEAS.md if it doesn't exist yet). Filing an idea away (Review mode
  only) archives it out of the active view within that same file — it isn't deleted and
  isn't shared. Promoting an idea is a separate, deliberate act that writes it (with
  added context) as its own new file under shared-ideas/, tracked in git and
  team-visible — each promoted idea gets its own file (not an entry in a shared list) so
  it can be read and iterated on independently. This skill has no knowledge of any
  downstream, org-specific destination for a shared idea (e.g. a proposal/spec process)
  — that's out of scope here by design, so this repo works the same way for anyone using
  it. No MCP required — uses Read/Write/Edit on the repo directly.
---

# Scratch Ideas

The point of this skill is to keep your own ideas list short and your attention on what's
active — filing something away is how you stay focused, not a rejection. Promotion to the
team is rare and deliberate: you don't share every idea, just the ones that survive a
second look.

This skill has two modes, and getting the mode right matters more than anything else
here. The goal of Quick mode is specifically to stop a random idea from becoming a
distraction: capture it in one exchange, then get straight back out of the way so the
user returns to whatever they were actually doing instead of drifting into idea-review.

## Step 0 — Pick the mode

- **Quick mode** — the ask is a bare capture phrase ("log this idea", "I have an idea",
  "add this to ideas") arising inside a conversation about something else entirely. Go to
  Step 1Q. One exchange, then get out of the way — no review, no nudge, no offer to file.
- **Review mode** — the user opened this thread specifically to work through their ideas
  ("review ideas", "what ideas am I sitting on", "file this idea away", "promote this
  idea", "kill this idea", "prune ideas"), or explicitly asks for anything beyond a bare
  capture. Go to Step 1R.
- If it's genuinely ambiguous (rare — most asks clearly fit one phrasing or the other),
  default to Quick mode. Under-reacting costs one follow-up question; over-reacting
  derails whatever the user was doing.

---

## Step 1Q — Quick mode: capture and get out of the way

**a. Find or create the target file.**
The target is `IDEAS.md` at the root of this repo (sibling to `templates/` and
`shared-ideas/`) — gitignored, personal, same pattern as `TODO.md`. If it doesn't exist
yet, create it by copying `templates/IDEAS.md`.

**b. Take the idea as given.** Don't ask clarifying questions unless the idea is
genuinely unintelligible — Quick mode optimizes for zero friction, not a polished entry.

**c. Capture the trigger point.**  
Since this idea is a side effect of whatever the running thread was actually doing, write
a `**Trigger:**` line yourself (don't ask the user for it) — one or two lines on what the
thread was working on and what happened in the last turn that sparked the idea. This is
what makes the entry legible later, once the surrounding conversation is long gone.

**d. Append it under `## Active`**, using this format exactly:

```
### <title>
**Captured:** <today's date, YYYY-MM-DD>  
**Status:** raw  
**Trigger:** <one or two lines: what the thread was doing, and what happened in the last
turn that sparked this idea>

<One or two lines: what the idea is and why it occurred to you.>

---
```

**e. Confirm in one short line** ("Logged.") and stop — no nudge, no review, no
suggestion to file it away. Filing, review, and promotion only happen in Review mode.

---

## Step 1R — Review mode: identify the intent

The user is doing one of five things. Identify which and jump to that step:

- **Capture** — they have a new idea to log → Step 2
- **Review** — they want to see what's active, or check what's been sitting too long → Step 3
- **File away** — they want to archive an idea out of active view → Step 4
- **Promote** — they want to share an idea with the team → Step 5
- **Prune** — they want to kill an idea entirely → Step 6

If it's ambiguous, do a quick review (Step 3) to orient, then ask.

---

## Step 2 — Capture a new idea (Review mode)

**2a. Find or create the target file.**  
The target is `IDEAS.md` at the root of this repo (sibling to `templates/` and
`shared-ideas/`) — gitignored, personal, same pattern as `TODO.md`. If it doesn't exist
yet, create it by copying `templates/IDEAS.md`.

**2b. Understand the idea.**  
Take what the user gave you — one sentence or five paragraphs, doesn't matter. If it's
vague, ask one clarifying question: *"What problem does this solve, or what made you
think of it?"* Don't over-interview. If they want to log it rough, log it rough.

**2c. Append it under `## Active`**, using this format exactly:

```
### <title>
**Captured:** <today's date, YYYY-MM-DD>  
**Status:** raw  

<One or two lines: what the idea is and why it occurred to you.>

---
```

Unlike Quick mode, don't fabricate a `**Trigger:**` line here — a dedicated ideas thread
usually has no other task running to point back to. Only add one if the user's own
message already names what prompted the idea.

Keep the body short — this is capture, not a spec.

**2d. After writing, go to Step 7 (nudge).**

---

## Step 3 — Review

**3a. Read `IDEAS.md`'s `## Active` section.** (Not `## Filed` — that's intentionally out
of the day-to-day view; only surface it if the user asks to see filed ideas specifically.)

**3b. Surface what's been sitting too long.**  
An idea that's been `raw` for more than 14 days without moving to `thinking` or being
filed is stale. Flag it clearly: *"[Title] has been raw since [date] — thought about it,
file it away, or kill it?"* If it has a `**Trigger:**` line, include it — that's the whole
point of capturing it: jogging the user's memory on an idea whose original context is
long gone from the conversation.

**3c. Count the Active list.**  
If it has more than 10 ideas, say so directly: *"You've got [N] active ideas. That's a lot
to keep in view — some of these probably want to be filed."*

**3d. After reviewing, go to Step 7 (nudge).**

---

## Step 4 — File an idea away

Filing isn't promotion — it's just getting an idea out of your active view without losing
it.

**4a. Identify which idea.** If the user named one, use it; otherwise ask which.

**4b. Move the entry** from `## Active` to `## Filed` in `IDEAS.md`, dropping the
`**Status:**` line (status only matters for the active list).

**4c. Confirm**, then go to Step 7 (nudge).

---

## Step 5 — Promote an idea to the team

This is the deliberate, occasional step — not something that happens on every capture.

**5a. Identify which idea.**  
Usually one from `## Filed` that the user is revisiting, but an idea can be promoted
straight from `## Active` if it's obviously share-worthy right away. If not named, ask.

**5b. Ask what changed.**  
Promotion should carry *why now* — what context, conversation, or realization made this
worth the team's attention. Ask directly: *"What's the context that makes this worth
sharing now?"* Don't skip this — it's what makes `shared-ideas/` worth reading instead of
becoming a second dumping ground.

**5c. Write it as its own file under `shared-ideas/`.**  
Filename is a kebab-case slug of the title (e.g. `link-discussion-sources.md`). Start from
`templates/shared-idea.md`'s shape:

```
# <Title>

**Promoted:** <today's date, YYYY-MM-DD>
**Context:** <what changed / what was learned that makes this worth sharing now>

<One or two lines: what the idea is.>
```

Unlike `IDEAS.md`'s single running list, this file is meant to be edited and expanded on
its own over time — don't cram it full up front; leave room for it to grow.

**5d. Remove the entry from `IDEAS.md`** (from the `###` header through the closing
`---`) — it now lives in `shared-ideas/`, not the personal list.

**5e. Confirm** what was written and where, then go to Step 7 (nudge).

Do not draft or write anything into any other repo as part of this step — promotion ends
at the new file in `shared-ideas/`. What an org does with a shared idea next is its own
process, outside this skill's scope.

---

## Step 6 — Prune (kill an idea)

Sometimes an idea just dies — from `## Active`, `## Filed`, or even `shared-ideas/`.

**6a. Identify what to kill.** The user may have named one, or you're acting on a stale
one surfaced during review. Ask: *"Kill it, or give it more time?"* — don't make them
justify the decision.

**6b. Remove it.**  
In `IDEAS.md` (`## Active` or `## Filed`): remove the entry, from the `###` header through
the closing `---`. In `shared-ideas/`: delete that idea's file entirely. No archive, no
graveyard. Gone.

**6c. Confirm**, then go to Step 7 (nudge).

---

## Step 7 — Nudge (always run this last)

After every interaction, end with a short, low-pressure nudge focused on the `## Active`
list — not `## Filed`, which is deliberately meant to sit without pressure.

Read the current state of `IDEAS.md`'s `## Active` section after any changes:

- If there are stale `raw` ideas: *"[Title] has been sitting since [date]. Thought about
  it, or should it get filed?"*
- If the list is clean: just say so — *"Active list looks healthy. Nothing stale."*
- Don't nudge about `## Filed` or `shared-ideas/` counts unless the user asked to review
  them this turn — pestering about filed ideas defeats the point of filing them away.

Keep it to one or two sentences. One concrete next action, not a meta-conversation about
idea hygiene.

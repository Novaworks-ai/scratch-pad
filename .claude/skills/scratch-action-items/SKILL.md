---
name: scratch-action-items
description: >
  Has two modes. Quick mode: use when the user drops a bare task ask — "add this to my
  todo", "add a todo to do X", "remind me to X" — with no transcript, often mid-conversation
  about something else entirely; just appends the item(s) to the current week's Tasks list
  in one exchange and gets back out of the way, nothing else. Transcript mode: use when the
  user hands over a meeting transcript (pasted text or a file) and wants their own personal
  action items pulled out, or wants to set/check this week's high-level Objectives.
  Triggers: "extract my action items from this transcript", "add my todos from this
  meeting", "what do I need to do from this call", "pull my action items out of this",
  "what are my objectives this week", "set my objectives for the week" — runs the full
  extract/flag-too-big/objectives-check/prune flow. Both modes only capture items that
  belong to the user themselves — not items assigned to other named participants. Appends
  to the current week's section of TODO.md at the scratch-pad repo root (gitignored,
  personal — created from templates/TODO.md if it doesn't exist yet). Each week's section
  starts with an Objectives list. Transcript mode also flags tasks that look too large for
  a quick TODO item (suggests they become a ticket instead) and suggests pruning the file
  once it's grown too big. No MCP required — uses Read/Write/Edit on the repo directly.
---

# Scratch Action Items

The point of Quick mode is to stop a stray task from derailing whatever the surrounding
conversation was actually doing: capture it in one exchange, then get straight back out
of the way and resume that other work — don't let capturing a to-do become the new focus.

## Step 0 — Pick the mode

- **Quick mode** — the ask is a bare task statement ("add this to my todo", "add a todo to
  buy X", "remind me to send Y") with no transcript attached, especially one dropped into a
  conversation about something else entirely. Go to Step 1Q.
- **Transcript mode** — the user handed over a meeting transcript (pasted text or a file)
  to extract action items from, or is explicitly working the Objectives-setting flow. Go to
  Step 1T.
- If genuinely ambiguous (rare), default to Quick mode — under-reacting costs one
  follow-up question; over-reacting turns a two-second ask into a multi-step ceremony.

---

## Step 1Q — Quick mode: capture and get back out of the way

**a. Find or create the target file, and this week's section.** Same file/section rules
as Transcript mode's Steps 1 and 5 below — reuse them, but if a brand-new week's section
is needed and the user hasn't stated objectives, don't stop to ask; leave the placeholder
bullet Step 5 describes and move straight on. Quick mode never blocks on Objectives.

**b. Take the task(s) as given.** No transcript to scan — just the item(s) the user
stated. Carry over a deadline if they mentioned one (`(Due: <date>)`). Skip duplicates
already in the list (checked or unchecked).

**c. Append each as a line** under that week's `Tasks:` header specifically — find that
literal `Tasks:` line within the current week's section, then add `- [ ] <task>` at the very
end of the checklist that follows it (after any existing items and any Transcript-mode
source sub-headings/groups under it), not anywhere else in the week's section (not above
`Tasks:`, not inside `Objectives:`, not between an existing sub-heading and its items).

**d. Silently note, don't ask, if a task doesn't map to a stated Objective** — mention it
in passing in your one-line confirmation (e.g. "neither maps to a stated Objective for
this week") rather than interrupting to check. Don't run Step 4's too-big-for-a-TODO flag
or Step 8's pruning nudge in Quick mode — those are Transcript-mode ceremony; a bare 1-2
item add doesn't need them unless a task is obviously, extremely large.

**e. Confirm in one short line** naming what got added, then continue exactly where the
surrounding conversation left off — no elaboration, no follow-up questions about
objectives or pruning.

**f. Watch the very next turn.** If the user's next message starts working the task just
captured (asking how to do it, drafting it, digging in) rather than moving on, don't just
follow along — that's the task quietly turning into active work without anyone deciding
to switch tracks. Ask directly: "Want to actually do this now, or should I leave it on the
TODO list and keep going?" Only treat it as genuinely new, unrelated work once real
conversation has happened since the capture.

---

## Step 1T — Transcript mode

### Step 1 — Find or create the target file

The target is `TODO.md` at the root of this repo (sibling to `templates/` and
`shared-notes/`), not `personal-notes/` or `shared-notes/`. If it doesn't exist yet, create
it by copying `templates/TODO.md`.

### Step 2 — Read the transcript

Take the transcript as pasted text or a file path the user gives you.

### Step 3 — Identify the user's own action items

Scan for action items assigned to the user specifically — by name, by direct address
("can you...", "you'll..."), or items they volunteered for. Skip action items assigned to
other named participants; skip vague discussion points that never became a commitment — a
discussion point isn't a task, it's an idea, and belongs in IDEAS.md via the companion
`scratch-ideas` skill instead (see the cross-check note in Step 9). If it's unclear whether
an item is the user's, ask rather than guess. Carry over any deadline mentioned in the
transcript as a `(Due: <date>)` tag on the task line.

Also identify what to call this transcript's source, for Step 7's grouping: a short label
for who/what the meeting was with (e.g. "Call with Eric" — from participant names or a
stated meeting title in the transcript), and the meeting's date. Take the date from the
transcript if it states or implies one (a timestamp, "today is...", a calendar reference);
otherwise use today's actual date. Don't ask the user for either — infer from the
transcript, falling back to today's date silently.

### Step 4 — Flag tasks that are too big for a TODO item

A personal TODO item should be doable in one sitting. If an extracted item reads like a
project rather than a task — spans multiple steps, needs other people, or would take more
than a day — don't just add it as a checklist line. Point it out to the user and suggest it
belongs as a ticket (GitHub issue or wherever the team tracks larger work) instead. Only add
it to TODO.md if the user still wants a personal placeholder for it.

### Step 5 — Find or start the current week's section, and its Objectives

Sections are organized by the calendar year's ISO week number (Monday–Sunday), newest week
first, headed `## Week N (<start date> - <end date>)` where N is today's actual ISO week
number — not a count of sections in the file. Determine today's ISO week number (e.g. `date
+%V`) and its Monday–Sunday date range.

- If a section for that week number already exists, use it — including whatever
  `Objectives:` list is already there (may be empty).
- If not, create a new `## Week N` section above the most recent existing one (newest on
  top), using the real ISO week number even if that skips numbers from the prior section.
  A brand-new section needs Objectives before tasks: ask the user for this week's 1-3
  high-level objectives (what they're trying to accomplish, not a task list) and write them
  under an `Objectives:` bullet list, matching `templates/TODO.md`'s shape. If they'd rather
  skip stating objectives this week, leave a single placeholder bullet noting that, and
  move on — don't block adding tasks on this.

### Step 6 — Check new items against this week's objectives

For each new task from Step 3 (or Step 4's user-confirmed too-big items), compare it
against the week's stated Objectives — does it plausibly serve one of them? This is a
loose, good-faith read, not a strict match. Add the task either way — don't withhold it —
but keep a running note of which new tasks didn't clearly map to any stated objective, to
surface in Step 8's summary rather than silently letting scope drift go unnoticed.

### Step 7 — Append to Tasks

Group this transcript's items under a source sub-heading, matching the existing style seen
in earlier weeks (e.g. `Call with Eric`): add a line `<source label> (<M/D>)` — using
Step 3's label and date — right before this transcript's checklist lines, with a blank line
before and after. Don't add a sub-heading for Quick-mode items or for any task with no
identifiable transcript source; those stay as plain lines directly under `Tasks:`.

Append each new item as a line in the existing checklist style: `- [ ] <task>`, adding
`(Due: <date>)` when a deadline applies. Keep tasks short and action-oriented (verb first).
Before adding, skim the existing list and skip anything that's a clear duplicate of what's
already there (checked or unchecked) — this includes skipping the sub-heading itself if an
identical one (same source and date) is already present, appending only the new lines
under it.

### Step 8 — Suggest pruning if the file has grown too big

If TODO.md has accumulated many weeks (roughly more than 6-8 sections) or feels long enough
that scanning it is a chore, say so and suggest pruning — e.g. archiving or deleting old
weeks that are fully checked off. Don't prune automatically; just flag it and let the user
decide.

### Step 9 — Confirm

Show the user the lines you added, which ones (if any) didn't clearly map to a stated
objective per Step 6, and anything flagged as too-big-for-a-TODO or skipped as a duplicate
— so they can adjust before moving on.

**Cross-check with `scratch-ideas`.** If Step 3 skipped anything as a vague discussion
point rather than a commitment, don't silently drop it — mention it here (e.g. "also saw 2
discussion points that weren't commitments — want me to run scratch-ideas on this
transcript to log those?"). Don't invoke that skill yourself; just flag it and let the
user decide.

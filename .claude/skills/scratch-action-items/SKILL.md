---
name: scratch-action-items
description: >
  Use this skill when the user hands over a meeting transcript (pasted text or a file) and
  wants their own personal action items pulled out and added to their TODO list. Triggers:
  "extract my action items from this transcript", "add my todos from this meeting", "what
  do I need to do from this call", "pull my action items out of this". Only extracts items
  that belong to the user themselves — not items assigned to other named participants.
  Appends new items to the current week's section of TODO.md at the scratch-pad repo root
  (gitignored, personal — created from templates/TODO.md if it doesn't exist yet). Also
  flags tasks that look too large for a quick TODO item (suggests they become a ticket
  instead) and suggests pruning the file once it's grown too big. No MCP required — uses
  Read/Write/Edit on the repo directly.
---

# Scratch Action Items

## Step 1 — Find or create the target file

The target is `TODO.md` at the root of this repo (sibling to `templates/` and
`shared-notes/`), not `personal-notes/` or `shared-notes/`. If it doesn't exist yet, create
it by copying `templates/TODO.md`.

## Step 2 — Read the transcript

Take the transcript as pasted text or a file path the user gives you.

## Step 3 — Identify the user's own action items

Scan for action items assigned to the user specifically — by name, by direct address
("can you...", "you'll..."), or items they volunteered for. Skip action items assigned to
other named participants; skip vague discussion points that never became a commitment. If
it's unclear whether an item is the user's, ask rather than guess. Carry over any deadline
mentioned in the transcript as a `(Due: <date>)` tag on the task line.

## Step 4 — Flag tasks that are too big for a TODO item

A personal TODO item should be doable in one sitting. If an extracted item reads like a
project rather than a task — spans multiple steps, needs other people, or would take more
than a day — don't just add it as a checklist line. Point it out to the user and suggest it
belongs as a ticket (GitHub issue or wherever the team tracks larger work) instead. Only add
it to TODO.md if the user still wants a personal placeholder for it.

## Step 5 — Append to the current week's section

Sections are organized by week (Monday–Sunday), newest week first, headed
`## Week N (<start date> - <end date>)`. Determine the current week from today's date:

- If a section for the current week already exists, append new items there.
- If not, create a new `## Week N` section above the most recent existing one (newest on
  top), incrementing N from the prior section.

For each new item, append a line in the existing checklist style: `- [ ] <task>`, adding
`(Due: <date>)` when a deadline applies. Keep tasks short and action-oriented (verb first).
Before adding, skim the existing list and skip anything that's a clear duplicate of what's
already there (checked or unchecked).

## Step 6 — Suggest pruning if the file has grown too big

If TODO.md has accumulated many weeks (roughly more than 6-8 sections) or feels long enough
that scanning it is a chore, say so and suggest pruning — e.g. archiving or deleting old
weeks that are fully checked off. Don't prune automatically; just flag it and let the user
decide.

## Step 7 — Confirm

Show the user the lines you added (and anything you flagged as too-big-for-a-TODO or
skipped as a duplicate) so they can adjust before moving on.

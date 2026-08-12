---
name: extract-action-items
description: >
  Use this skill when the user hands over a meeting transcript (pasted text or a file) and
  wants their own personal action items pulled out and added to their TODO list. Triggers:
  "extract my action items from this transcript", "add my todos from this meeting", "what
  do I need to do from this call", "pull my action items out of this". Only extracts items
  that belong to the user themselves — not items assigned to other named participants.
  Appends new items to TODO.md at the scratch-pad repo root (gitignored, personal —
  created from templates/TODO.md if it doesn't exist yet). No MCP required — uses
  Read/Write/Edit on the repo directly.
---

# Extract Action Items

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
it's unclear whether an item is the user's, ask rather than guess.

## Step 4 — Append to TODO.md

For each new item, append a line in the existing checklist style: `- [ ] <task>`. Keep
tasks short and action-oriented (verb first). Before adding, skim the existing list and
skip anything that's a clear duplicate of what's already there (checked or unchecked).

## Step 5 — Confirm

Show the user the lines you added (and any items you skipped as ambiguous or
already-present) so they can adjust before moving on.

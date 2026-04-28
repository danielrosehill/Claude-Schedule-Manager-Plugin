---
name: firehose
description: Take a free-form mixed dump of items and route each into Google Calendar (events) or Todoist (tasks). Confirms the split with the user before writing.
---

# Firehose

User provides a mixed brain-dump (voice-transcribed or typed). Each item is either an **appointment** (specific time/place, has attendees, blocks calendar) or a **task** (work to do, has a due date at most). Classify, confirm, then create.

## Steps

1. **Read config** per `lib/CONFIG.md`. Abort with onboarding pointer if missing.

2. **Parse the dump** into individual items. Strip filler.

3. **Classify each item** as `event`, `task`, or `unclear`. Heuristics:
   - Specific time + duration + (optional) attendee → `event`
   - Action verb + due-by phrasing, no fixed time → `task`
   - Vague ("think about X") → `task` with no date
   - Time-blocked focus work without external attendees → user's call (ask)

4. **Present the split** as a table to the user before writing anything:
   | # | Item | Route | Details (when, who, project) |

5. **Get confirmation or corrections.** User can flip routing per row, edit details, or drop rows.

6. **Create in batches.** Delegate to:
   - `batch-create-events` for the event rows
   - `batch-create-tasks` for the task rows
   - For events with attendees, resolve names via the contacts MCP first.

7. **Report** what was created with links to the new event(s) and task(s).

## Notes

- Never write without explicit user confirmation of the split.
- If an item's date/time is ambiguous, ask once; do not silently assume.
- Default timezone from `config.defaults.timezone`.

---
name: task-to-event
description: Migrate a Todoist task into a Google Calendar event — two-part: create the event, then delete the task. Useful when something captured as a task should actually be on the calendar.
---

# Task → Event Migration

## Steps

1. **Read config.** Workspace MCP, Todoist MCP, contacts MCP.

2. **Identify the task(s).** Accept one or many Todoist tasks (ID, URL, or fuzzy reference).

3. **Gather missing event fields.** A task likely lacks: start time, duration, attendees, location. Ask the user for each missing field per task, or accept defaults (e.g., 30 min, no attendees).

4. **Confirm the migration plan** as a table:
   | Task | → Event title | When | Attendees |

5. **Create events first** (delegate to `create-event` or `batch-create-events`).

6. **Verify creation succeeded.** Capture the new event IDs.

7. **Delete the source tasks** only after every corresponding event is confirmed created. If any event creation failed, leave its task in place and report.

8. **Report** per-row: new event link + "task deleted" or "event failed, task preserved".

## Notes

- This is a two-part operation; **never delete before the event exists**. A failure mid-way must leave the user with no data lost.
- Confirm explicitly before deleting tasks — the user may want to keep them for tracking.

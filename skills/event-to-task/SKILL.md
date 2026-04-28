---
name: event-to-task
description: Migrate a Google Calendar event into a Todoist task — two-part: create the task, then delete the event. For things miscaptured as appointments.
---

# Event → Task Migration

## Steps

1. **Read config.** Workspace MCP, Todoist MCP.

2. **Identify the event(s).** Accept ID, URL, or fuzzy reference.

3. **Gather missing task fields.** An event likely lacks: priority, project, labels. The event's title becomes the task content; description carries over to task notes; start date becomes the task due (unless user wants no date).

4. **Confirm the migration plan** as a table:
   | Event | → Task content | Due | Project | Priority |

5. **Create tasks first** (delegate to `create-task` or `batch-create-tasks`).

6. **Verify creation succeeded.** Capture new task IDs.

7. **Delete events only after confirmation.** Warn if the event has attendees — deletion sends cancellation notices. If attendees exist, ask whether to delete (sending notices) or just remove the user from the invite.

8. **Report** per-row: new task link + event deletion status.

## Notes

- Two-part operation; never delete before the task exists.
- Be especially careful with events that have attendees — cancellations are visible and irreversible.

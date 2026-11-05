---
name: delete-task
description: Delete a Todoist task. Confirms before deleting; offers complete-instead for tasks that look done.
---

# Delete Todoist Task

## Steps

1. **Read config.** Todoist calls go through the REST API (see `lib/CONFIG.md`).

2. **Identify the task** (ID, URL, or fuzzy reference — see `edit-task`).

3. **Show task details.**

4. **Sanity check.** If the task content suggests it's actually done ("Wrote the report", "Sent email to X"), offer to mark it complete instead of deleting. Completion preserves history; deletion does not.

5. **Confirm.** Require explicit "yes, delete" before proceeding.

6. **Delete** via `DELETE /tasks/<id>` (or `POST /tasks/<id>/close` if completing instead). Report result.

## Notes

- This is destructive and removes the task from history. Always confirm.
- Use `task-to-event` if the user actually wants to migrate the task to a calendar event rather than just delete it.

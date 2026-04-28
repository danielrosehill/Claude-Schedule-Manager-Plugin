---
name: edit-task
description: Modify an existing Todoist task — content, due, priority, project, labels. Identifies the task by ID, link, or fuzzy match.
---

# Edit Todoist Task

## Steps

1. **Read config.** Todoist MCP alias.

2. **Identify the task.** Accept:
   - Direct task ID
   - Todoist URL (parse the task ID)
   - Fuzzy reference: "the task about X" → search recent open tasks, present matches, let user confirm

3. **Show current state** before editing.

4. **Apply changes.** Common: reschedule due, change priority, move project, edit content, add/remove labels.

5. **Update** via Todoist MCP. Report the updated task.

## Notes

- For completing a task, prefer Todoist's UI / its dedicated complete operation — this skill is for non-completion edits.
- For priority sweeps across many tasks, use `assign-priorities`.
- For date sweeps, use `assign-dates`.

---
name: create-task
description: Create a single Todoist task. Sets project, due date, priority, labels per user input or sensible defaults.
---

# Create Todoist Task

## Steps

1. **Read config.** Todoist MCP alias and `defaults.todoist_project_id`.

2. **Gather fields:**
   - Content (required) — the task description
   - Due (date, datetime, or natural-language string Todoist accepts)
   - Project (default `defaults.todoist_project_id`, falls back to inbox)
   - Priority (1–4; Todoist convention: 1 = highest, 4 = none)
   - Labels (optional)
   - Description / notes (optional)

3. **Confirm** if the task is going somewhere other than the default project.

4. **Create** via Todoist MCP. Capture task ID and URL.

5. **Report** the task link.

## Notes

- For multi-task creation, use `batch-create-tasks`.
- If the user says "high priority" without a number, map to priority 1.
- If priority or due date is missing on a task that probably needs one, do not auto-fill — `assign-priorities` and `assign-dates` exist for that.

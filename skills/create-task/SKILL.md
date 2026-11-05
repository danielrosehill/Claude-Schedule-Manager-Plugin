---
name: create-task
description: Create a single Todoist task. Sets project, due date, priority, labels per user input or sensible defaults.
---

# Create Todoist Task

## Steps

1. **Read config.** `defaults.todoist_project_id`. Todoist calls go through the REST API (see `lib/CONFIG.md`).

2. **Gather fields:**
   - Content (required) — the task description
   - Due (date, datetime, or natural-language string Todoist accepts)
   - Project (default `defaults.todoist_project_id`, falls back to inbox)
   - Priority (API `4` = p1 urgent … `1` = none)
   - Labels (optional)
   - Description / notes (optional)

3. **Confirm** if the task is going somewhere other than the default project.

4. **Create** via `POST /tasks`. Capture task ID and URL (`https://app.todoist.com/app/task/<id>`).

5. **Report** the task link.

## Notes

- For multi-task creation, use `batch-create-tasks`.
- If the user says "high priority" without a number, map to API priority 4 (p1).
- If priority or due date is missing on a task that probably needs one, do not auto-fill — `assign-priorities` and `assign-dates` exist for that.

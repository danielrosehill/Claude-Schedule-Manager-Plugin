---
name: batch-create-tasks
description: Create multiple Todoist tasks from a structured list. Confirms the table, then writes serially.
---

# Batch Create Todoist Tasks

## Steps

1. **Read config.** `defaults.todoist_project_id`. Todoist calls go through the REST API (see `lib/CONFIG.md`).

2. **Accept the batch** — structured list from the user, or invoked by `firehose` with the task subset.

3. **Normalise rows** to the same fields as `create-task`. Fill default project where unspecified.

4. **Show the table** for user confirmation. Flag rows missing priority or due if they look like they should have one (heuristic: action verb + concrete deliverable). Don't auto-fill — just flag, and offer to chain `assign-priorities` / `assign-dates` after creation.

5. **Create tasks serially** via `POST /tasks`, one call per row. On per-row failure, continue and collect.

6. **Report** per-row result: link if created, error if failed.

## Notes

- Todoist's API tolerates parallel writes but enforces rate limits. Stay serial; correctness over speed.
- After batch creation, prompt the user whether to run `assign-priorities` / `assign-dates` on the new tasks.

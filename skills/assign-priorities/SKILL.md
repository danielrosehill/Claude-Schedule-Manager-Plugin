---
name: assign-priorities
description: Assign priorities to Todoist tasks in batch. Walks the user through each unprioritised task and applies their choice.
---

# Assign Priorities

## Steps

1. **Read config.** Todoist calls go through the REST API (see `lib/CONFIG.md`).

2. **Get the working set.** Either:
   - Handed in from `review-missing-priorities`
   - Freshly queried (default: all open tasks with no priority, `GET /tasks/filter?query=p4`)

3. **Walk the list interactively.** For each task, present:
   - Content + project + due date
   - Prompt for priority (p1 = urgent, p2, p3, or skip)

   Support batch shortcuts: "all due this week → 2", "all in Project X → 3", etc. Build the assignment map first, then apply.

4. **Confirm the assignment table** before writing.

5. **Apply updates serially** via `POST /tasks/<id>` with `priority`. On per-task failure, continue and collect.

6. **Report** per-task result.

## Notes

- The API numbers priority against the UI: p1 (urgent) = API `4`, p2 = `3`, p3 = `2`, none = `1`. Translate before writing.
- Don't auto-assign based on heuristics. The user picks.

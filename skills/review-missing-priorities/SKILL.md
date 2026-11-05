---
name: review-missing-priorities
description: Audit Todoist for tasks lacking a priority. Read-only — produces a list and recommends running assign-priorities.
---

# Review Tasks Missing Priorities

## Steps

1. **Read config.** Todoist calls go through the REST API (see `lib/CONFIG.md`).

2. **Define scope.** Ask the user (or accept arguments):
   - All open tasks (default)
   - One project
   - Tasks due in a date range

3. **Query Todoist** for tasks in scope (`GET /tasks/filter?query=p4`, or `GET /tasks` and keep `priority == 1`, which is the API's "no priority").

4. **Present the list** as a table grouped by project:
   | Project | Task | Due | Created |

5. **Suggest next step.** Offer to run `assign-priorities` over the listed tasks, or hand off the list to the user for manual review.

## Notes

- This skill is read-only. It never modifies tasks.
- In the API, priority `1` is the default "no priority" (the UI shows it as p4) — that's what we audit for.

---
name: review-missing-priorities
description: Audit Todoist for tasks lacking a priority. Read-only — produces a list and recommends running assign-priorities.
---

# Review Tasks Missing Priorities

## Steps

1. **Read config.** Todoist MCP alias.

2. **Define scope.** Ask the user (or accept arguments):
   - All open tasks (default)
   - One project
   - Tasks due in a date range

3. **Query Todoist** for tasks in scope. Filter to those with priority 4 (Todoist's "no priority").

4. **Present the list** as a table grouped by project:
   | Project | Task | Due | Created |

5. **Suggest next step.** Offer to run `assign-priorities` over the listed tasks, or hand off the list to the user for manual review.

## Notes

- This skill is read-only. It never modifies tasks.
- Todoist treats priority 4 as the default "no priority" — that's what we audit for.

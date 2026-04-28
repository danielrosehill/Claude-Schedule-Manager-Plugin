---
name: review-missing-dates
description: Audit Todoist for tasks lacking a due date. Read-only — produces a list and recommends running assign-dates.
---

# Review Tasks Missing Dates

## Steps

1. **Read config.** Todoist MCP alias.

2. **Define scope.** Ask (or accept arguments):
   - All open tasks (default)
   - One project
   - Tasks created before a cutoff (stale-task audit)

3. **Query Todoist.** Filter to tasks with no due date.

4. **Present the list** as a table grouped by project:
   | Project | Task | Priority | Created |

5. **Suggest next step.** Offer to run `assign-dates` over the list, or hand off for manual review.

## Notes

- Read-only. No writes.
- Some tasks legitimately have no date (someday-maybe items). Surface that to the user before they bulk-assign.

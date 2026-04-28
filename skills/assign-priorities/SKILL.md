---
name: assign-priorities
description: Assign priorities to Todoist tasks in batch. Walks the user through each unprioritised task and applies their choice.
---

# Assign Priorities

## Steps

1. **Read config.** Todoist MCP alias.

2. **Get the working set.** Either:
   - Handed in from `review-missing-priorities`
   - Freshly queried (default: all open priority-4 tasks)

3. **Walk the list interactively.** For each task, present:
   - Content + project + due date
   - Prompt for priority (1 = highest, 2, 3, or skip)

   Support batch shortcuts: "all due this week → 2", "all in Project X → 3", etc. Build the assignment map first, then apply.

4. **Confirm the assignment table** before writing.

5. **Apply updates serially** via Todoist MCP. On per-task failure, continue and collect.

6. **Report** per-task result.

## Notes

- Priority 1 = highest in Todoist (counter-intuitive — confirm the user's mental model on first run).
- Don't auto-assign based on heuristics. The user picks.

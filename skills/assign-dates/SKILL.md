---
name: assign-dates
description: Assign due dates to Todoist tasks in batch. Walks the user through each undated task and applies their choice.
---

# Assign Dates

## Steps

1. **Read config.** Todoist MCP alias.

2. **Get the working set.** Either handed in from `review-missing-dates`, or freshly queried (default: all open undated tasks).

3. **Walk the list interactively.** For each task, prompt for:
   - Specific date / datetime, or
   - Natural-language string Todoist parses ("next Monday", "in 3 days"), or
   - Skip (leave undated — explicitly someday/maybe)

   Support batch shortcuts: "all in Project X → next Friday", "all priority 1 → tomorrow".

4. **Confirm the assignment table.**

5. **Apply serially** via Todoist MCP. Collect failures.

6. **Report** per-task result.

## Notes

- Use `defaults.timezone` for date interpretation.
- Don't infer dates from task content automatically — the user picks.

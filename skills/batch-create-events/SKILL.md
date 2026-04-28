---
name: batch-create-events
description: Create multiple Google Calendar events from a structured list. Resolves attendees once across the batch, confirms the table, then writes.
---

# Batch Create Calendar Events

## Steps

1. **Read config.** Workspace MCP, contacts MCP, defaults.

2. **Accept the batch** — either user provides a structured list (table, JSON, markdown) or this skill is invoked by `firehose` with the event subset.

3. **Normalise rows** to the same fields as `create-event`. Fill defaults (calendar, duration, timezone).

4. **Resolve attendees in bulk.** Deduplicate name lookups so the contacts MCP isn't called per row for repeating people. Present any ambiguous matches as a single resolution pass.

5. **Show the full table** for user confirmation. Allow row edits before write.

6. **Create events serially** via workspace MCP. If any single row fails, continue and collect failures rather than aborting the whole batch.

7. **Report** a per-row result: link if created, error if failed.

## Notes

- Calendar APIs throttle; a small delay between writes is fine. Prefer correctness over throughput.
- Don't attempt parallel writes — the workspace MCP isn't guaranteed concurrency-safe.

---
name: minutes
description: Manage meeting minutes as Google Docs — capture from a discussion, share with attendees, or email. One skill, three sub-actions.
---

# Minutes

Single skill, three sub-actions: `capture`, `share`, `email`. The user names the action; if absent, ask.

## Sub-actions

### `capture`

Create or update a minutes doc for a meeting (past or in-progress).

1. **Read config.** Workspace MCP, `drive_folders.minutes`.
2. **Identify the event** (ID, URL, or fuzzy reference).
3. **Locate or create the doc.** Look for an agenda already linked in the event description (`agenda link` action). If found, append a "Minutes" section to that doc — agenda → minutes single-document flow. If no agenda exists, create a new Doc in `drive_folders.minutes` titled `Minutes — <event title> — YYYY-MM-DD`.
4. **Structure the minutes:**
   - Attendees (from the event)
   - Decisions made
   - Action items (with owner + due date if known)
   - Open questions
   - Notes / verbatim
5. **Push action items to Todoist** if any were captured. Use `batch-create-tasks` with the action-item rows. Confirm before pushing.
6. **Update the event description** (if not already linked) with the minutes doc link.

### `share`

Share a minutes doc with the event's attendees via Drive permissions.

1. **Identify the minutes doc and the event.**
2. **Resolve attendees** from the invite list.
3. **Set permissions** (default role `viewer` for minutes; ask for `commenter` if the user wants follow-up discussion).
4. **Confirm** the share list before writing.

### `email`

Email the minutes doc to attendees (or user-specified list) via Gmail.

1. **Identify doc and recipients.**
2. **Compose** with subject `Minutes — <event title> — YYYY-MM-DD` and a short body summarising decisions + action items, plus a link.
3. **Send** via workspace MCP's Gmail tool. Confirm before sending.

## Notes

- Prefer the single-doc agenda → minutes flow when an agenda already exists. Do not create a duplicate doc unless the user explicitly asks.
- `link` action isn't separate here because `capture` always links the doc to the event automatically.
- Action items pushed to Todoist must be confirmed by the user — don't silently write tasks.

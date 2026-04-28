---
name: delete-event
description: Delete a Google Calendar event. Confirms before deleting; warns when attendees will receive cancellation notices.
---

# Delete Calendar Event

## Steps

1. **Read config.** Workspace MCP alias.

2. **Identify the event** (ID, URL, or fuzzy reference — see `edit-event` for the resolution flow).

3. **Show event details** including attendee list.

4. **Warn the user** if attendees are present — deletion sends cancellation notices.

5. **Confirm.** Require explicit "yes, delete" before proceeding.

6. **Delete** via workspace MCP. Report result.

## Notes

- This is destructive and visible to other people. Always confirm.
- For recurring events, ask whether to delete just this instance, all future, or the whole series.

---
name: edit-event
description: Modify an existing Google Calendar event — time, attendees, description, location. Identifies the event by user-provided reference (link, ID, or fuzzy match).
---

# Edit Calendar Event

## Steps

1. **Read config.** Workspace MCP alias.

2. **Identify the event.** Accept any of:
   - Direct event ID
   - Calendar URL (parse the eid)
   - Fuzzy reference: "the meeting with X tomorrow" → search recent events, present matches, let user confirm

3. **Show current state** of the event before editing.

4. **Apply changes.** Common ones: reschedule (time/duration), add/remove attendees (resolve names via contacts MCP), update description, change location.

5. **Confirm before writing** if multiple fields changing or if the change touches attendees (which fires invite emails).

6. **Update** via workspace MCP. Report the updated event link.

## Notes

- For batched edits, just run this skill in sequence — there is no `batch-edit-events` (rare use case; not worth the surface).
- Reschedules send updated invites by default. Mention this to the user when attendees are present.

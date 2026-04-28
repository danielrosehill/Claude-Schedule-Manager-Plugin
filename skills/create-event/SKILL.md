---
name: create-event
description: Create a single Google Calendar event. Resolves attendees via the contacts MCP. Optionally links a Drive doc (agenda) into the description.
---

# Create Calendar Event

## Steps

1. **Read config.** Resolve workspace MCP alias, contacts MCP alias, and `defaults.calendar_id`/`defaults.timezone`.

2. **Gather event fields** from the user (or arguments):
   - Title (required)
   - Start, end (or duration); default duration 30 min if not given
   - Calendar (default `defaults.calendar_id`)
   - Description (optional)
   - Location (optional)
   - Attendees (optional — names or emails)

3. **Resolve attendees.** For any attendee given as a name, query the contacts MCP. If the lookup is ambiguous, present matches and let the user pick. If no match, ask for an email.

4. **Confirm** the resolved event payload before writing.

5. **Create** via the workspace MCP's calendar event creation tool. Capture the event ID and URL.

6. **Report** the link.

## Notes

- For multi-event creation, use `batch-create-events` instead.
- For events that need an agenda doc, follow up with `agenda` (action: `create`, then `link`).
- Default to inviting attendees as "guests" without requiring response unless user specifies otherwise.

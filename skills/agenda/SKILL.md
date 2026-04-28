---
name: agenda
description: Manage meeting agendas as Google Docs — create, link to a calendar event description, share with attendees, or email. One skill, four sub-actions.
---

# Agenda

Single skill, four sub-actions: `create`, `link`, `share`, `email`. The user names the action when invoking; if absent, ask.

## Sub-actions

### `create`

Create a new Google Doc agenda for an upcoming event.

1. **Read config.** Workspace MCP, `drive_folders.agendas`.
2. **Identify the event** (ID, URL, or fuzzy reference).
3. **Generate doc title:** `Agenda — <event title> — YYYY-MM-DD`.
4. **Apply template:**
   - Header: event title, date/time, attendees
   - Sections: Objectives, Discussion items, Decisions needed, Action items, Notes
5. **Create the Doc** in `drive_folders.agendas` via workspace MCP. Return the link.
6. **Offer to chain** `link` next.

### `link`

Add an agenda doc link to a calendar event's description.

1. **Identify the event and the doc.**
2. **Read current event description.** Append (don't overwrite) a labelled link: `Agenda: <doc URL>`.
3. **Update the event** via workspace MCP.

### `share`

Share an agenda doc with the event's attendees via Google Drive permissions.

1. **Identify the agenda doc.** If user gives the event, find its linked agenda by parsing the description, or fall back to title match in `drive_folders.agendas`.
2. **Resolve attendees** from the event invite list. (If users want non-attendee shares, they specify.)
3. **Set permissions** via workspace MCP — default role `commenter`, ask if user wants `editor` or `viewer`.
4. **Confirm** the share list before writing.

### `email`

Email an agenda doc as a link (or attached PDF, on request) via Gmail.

1. **Identify the agenda doc and the recipients** (event attendees by default, or user-provided list).
2. **Compose** a short email with:
   - Subject: `Agenda — <event title>`
   - Body: short note, link to the Doc
3. **Send** via workspace MCP's Gmail tool. Confirm before sending.

## Notes

- Sub-action dispatch is at the top of the body. Keep it tight.
- The `link` step appends rather than overwrites — events may already carry meeting URLs (Meet/Zoom).
- Sharing and emailing both involve external visibility. Always confirm the recipient list.

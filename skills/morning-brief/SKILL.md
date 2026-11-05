---
name: morning-brief
description: Brief on where you left off — reads the most recent wrapup doc and overlays today's calendar and open Todoist tasks.
---

# Morning Brief

Picks up from the most recent `wrapup` and surfaces today's load.

## Steps

1. **Read config.** Resolve workspace MCP, `drive_folders.wrapups`, and (optionally) `drive_folders.morning_briefs`.

2. **Find the most recent wrapup** in the wrapups folder by created/modified date. Read its body.

3. **Pull today's load:**
   - Calendar events for today
   - Todoist tasks due today + overdue (`GET /tasks/filter?query=today | overdue`, REST API per `lib/CONFIG.md`)

4. **Compose the brief:**
   - **Where you left off:** Open items + final notes from the most recent wrapup
   - **Today's calendar:** Events with times and attendees
   - **Today's tasks:** Due + overdue with priorities

5. **Output options:**
   - Inline in the chat (default)
   - Optionally save as a Doc in `drive_folders.morning_briefs` if the user opted in during onboarding
   - Optionally email to self (reuse email helper)

## Notes

- This skill is read-only to Calendar and Todoist. It never marks tasks complete or modifies events.
- If no wrapup exists yet, brief on calendar + tasks only and tell the user to start using `wrapup` for end-of-day continuity.

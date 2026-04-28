---
name: wrapup
description: Produce an end-of-day, end-of-week, or end-of-period summary as a Google Doc in the Wrapups folder. Lists achievements and open items.
---

# Wrapup

Generates a structured Google Doc summarising what got done in a period and what's still open. The cadence is user-driven — daily, weekly, end-of-project, whatever.

## Steps

1. **Read config.** Resolve workspace MCP alias and `drive_folders.wrapups`.

2. **Determine period.** Ask the user (or accept from arguments): EOD today, EOW this week, custom range. Resolve start/end timestamps in `config.defaults.timezone`.

3. **Pull source data** for the period:
   - Calendar events (attended, with attendees)
   - Todoist completed tasks
   - Todoist tasks still open with due dates inside the period (carry-overs)

4. **Draft sections:**
   - **Header:** period label + date stamp
   - **Achievements:** completed tasks + significant events
   - **Open items:** unfinished tasks (with due dates), commitments made in meetings
   - **Notes:** free-text section the user can extend

5. **Create the Doc** in `drive_folders.wrapups`. Naming: `Wrapup — <period label> — YYYY-MM-DD`.

6. **Return the Doc link** to the user. Optionally offer to email it via `email-agenda`-style flow (reuse the email helper if available).

## Notes

- This is read-write to Drive but read-only to Calendar/Todoist. Don't mark tasks complete or modify events from within wrapup.
- Morning-brief reads the most recent wrapup; keep the structure stable so morning-brief can parse it.

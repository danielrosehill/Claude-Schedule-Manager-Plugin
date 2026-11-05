---
name: onboard
description: First-run setup for Schedule-Manager. Picks MCP aliases, creates Drive folder tree, optionally nominates a diary workspace, writes config.json.
---

# Onboard Schedule-Manager

Run this once before any other Schedule-Manager skill. Subsequent skills require `$CLAUDE_USER_DATA/schedule-manager/config.json` to exist.

## Steps

1. **Resolve data root.**
   ```bash
   DATA_ROOT="${CLAUDE_USER_DATA:-${XDG_DATA_HOME:-$HOME/.local/share}/claude-plugins}/schedule-manager"
   mkdir -p "$DATA_ROOT"
   ```

2. **Pick MCP aliases.** Ask the user for the MCP server aliases configured in their environment for:
   - Google Workspace (Calendar, Docs, Gmail) — recommend `gemini-cli-extensions/workspace`.
   - Contacts (Google People API) — recommend the companion `Diary-Contacts-MCP` or any People API MCP.

   Verify each alias resolves to a tool list including the expected capabilities. If a given MCP isn't registered, tell the user how to add it; do not proceed without both.

   Todoist needs no MCP: skills call the REST API with `TODOIST_API_KEY`. Check it is available (`with-secrets --list`, or the env var) and test with `GET https://api.todoist.com/api/v1/projects?limit=1`.

3. **Create Drive folder tree.** Using the workspace MCP, create (or locate) folders under a root the user nominates (default name `Schedule-Manager`):
   - `Agendas`
   - `Minutes`
   - `Wrapups`
   - `Morning-Briefs` (optional, ask)

   Capture each folder ID for `config.json`.

4. **Diary workspace (optional).** Ask the user if they want a markdown diary. If yes, ask for an absolute path (suggest `~/Documents/Diary` or a synced folder; do not default to `$CLAUDE_USER_DATA`). Verify the folder exists or create it. If no, set `diary.enabled = false`.

5. **Defaults.** Confirm calendar (default `primary`), Todoist project (default `inbox`), timezone (default user's locale).

6. **Write `config.json`** following the schema in `lib/CONFIG.md`. Use chmod 600 on the file.

7. **Tell the user** what was written and which skills are now ready. Mention `setup-automation` for hooking up morning-brief / wrapup on a schedule.

## Re-running onboard

Re-running should detect existing config and offer to update individual sections (MCP aliases, folder IDs, diary workspace) rather than overwriting blindly.

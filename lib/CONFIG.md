# Schedule-Manager — shared config reference

Every skill reads `$CLAUDE_USER_DATA/schedule-manager/config.json`. If it's missing, point the user at the `onboard` skill.

## Resolution

```bash
DATA_ROOT="${CLAUDE_USER_DATA:-${XDG_DATA_HOME:-$HOME/.local/share}/claude-plugins}/schedule-manager"
CONFIG="$DATA_ROOT/config.json"
```

## Schema

```json
{
  "mcp": {
    "workspace": "<MCP alias for Google Workspace MCP — calendar/docs/gmail>",
    "contacts": "<MCP alias for the Contacts MCP — Google People API>"
  },
  "drive_folders": {
    "agendas": "<Drive folder ID>",
    "minutes": "<Drive folder ID>",
    "wrapups": "<Drive folder ID>",
    "morning_briefs": "<Drive folder ID, optional>"
  },
  "diary": {
    "enabled": false,
    "path": "<absolute path to user-nominated folder for markdown diary entries; null if disabled>"
  },
  "defaults": {
    "calendar_id": "primary",
    "todoist_project_id": null,
    "timezone": "Asia/Jerusalem"
  }
}
```

## MCP-call pattern

Skills don't hardcode MCP tool names for Google. They read `config.mcp.<service>` (`workspace`, `contacts`) to get the alias, then invoke `mcp__<alias>__<tool>` accordingly. This lets the user pick whichever workspace/contacts MCP they prefer without forking the plugin.

## Todoist REST pattern

Todoist is not an MCP here. There is no `config.mcp.todoist`; an old one in `config.json` is ignored. Skills call the Todoist REST API v1 with `curl`:

- Base `https://api.todoist.com/api/v1`, header `Authorization: Bearer $TODOIST_API_KEY`. The key is in Infisical; run as `with-secrets bash -c 'curl -s ... -H "Authorization: Bearer $TODOIST_API_KEY" ...'`. Never print the key or write it to a file.
- Create: `POST /tasks` with `{content, description, project_id, section_id, parent_id, labels, priority, due_string | due_date | due_datetime, deadline_date}`. Omit `project_id` for the Inbox.
- Read: `GET /tasks?project_id=&label=&ids=` or `GET /tasks/filter?query=<Todoist filter>` (e.g. `no date`, `today | overdue`, `p4`). Paged: `{"results": [...], "next_cursor": ...}`; pass `cursor=` until null; `limit` up to 200.
- Update: `POST /tasks/<id>` with only the fields to change. Move: `POST /tasks/<id>/move`. Complete: `POST /tasks/<id>/close`. Reopen: `POST /tasks/<id>/reopen`. Delete: `DELETE /tasks/<id>`.
- Completed in a window: `GET /tasks/completed/by_completion_date?since=<ISO UTC>&until=<ISO UTC>` (max 3 months; response key is `items`).
- Projects: `GET /projects`, `GET /projects/search?query=<name>` (literal match; `*` is a wildcard). Labels: `GET /labels`.
- Priority is inverted against the UI: API `4` = p1 (urgent), `3` = p2, `2` = p3, `1` = none (the default for new tasks).
- Tested read-only on 2026-11-05: tasks, tasks/filter, completed/by_completion_date, projects, projects/search, labels. Write endpoints are from developer.todoist.com/api/v1 and were not run.

## Failure mode

If `config.json` is missing, every skill should:

1. Tell the user the plugin isn't onboarded.
2. Suggest they run the `onboard` skill.
3. Stop.

Do not auto-create `config.json` outside `onboard`.

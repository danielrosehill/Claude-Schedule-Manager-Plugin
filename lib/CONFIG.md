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
    "contacts": "<MCP alias for the Contacts MCP — Google People API>",
    "todoist": "<MCP alias for Todoist MCP>"
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

Skills don't hardcode MCP tool names. They read `config.mcp.<service>` to get the alias, then invoke `mcp__<alias>__<tool>` accordingly. This lets the user pick whichever workspace/todoist/contacts MCP they prefer without forking the plugin.

## Failure mode

If `config.json` is missing, every skill should:

1. Tell the user the plugin isn't onboarded.
2. Suggest they run the `onboard` skill.
3. Stop.

Do not auto-create `config.json` outside `onboard`.

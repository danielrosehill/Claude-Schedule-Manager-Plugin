# Schedule-Manager

Claude Code plugin for personal schedule, task, and meeting management. Routes mixed brain-dumps into Google Calendar events and Todoist tasks; manages agenda/minutes Google Docs linked to events; produces wrapup logs and morning briefs.

## What it does

- **Firehose**: drop a mixed list of items, the plugin classifies each as event vs task and creates them in the right service after confirmation.
- **Calendar CRUD**: create, edit, delete, batch-create events. Resolves attendees via a Contacts MCP.
- **Todoist CRUD**: create, edit, delete, batch-create tasks.
- **Migration**: `task-to-event` and `event-to-task` for items captured in the wrong service.
- **Hygiene**: audit and bulk-assign missing priorities and due dates in Todoist.
- **Meetings**: agenda and minutes lifecycle as Google Docs, linked to events, shareable via Drive or Gmail.
- **Day cycle**: `wrapup` (EOD/EOW summary as a Doc) + `morning-brief` (resume from last wrapup, overlay today's load).
- **Diary** (optional): markdown entries to a user-nominated folder.

## Dependencies

The plugin doesn't bundle MCPs — the user wires up two separately and the plugin reads their aliases from `config.json`. Todoist is called directly through its REST API v1 (no MCP):

| Capability | Recommended MCP |
|---|---|
| Google Calendar, Docs, Gmail | [`gemini-cli-extensions/workspace`](https://github.com/gemini-cli-extensions/workspace) (Google official) |
| Google Contacts (People API) | A standalone Contacts MCP (e.g., the companion `Diary-Contacts-MCP`) |
| Todoist | none: REST API v1 with `curl`, key `TODOIST_API_KEY` (Infisical, run under `with-secrets`). See `lib/CONFIG.md` |

Any equivalent MCP works for Google — the plugin only cares about the alias mapped in `config.json`.

## Skills

| Skill | What it does |
|---|---|
| `onboard` | First-run setup: pick MCP aliases, create Drive folder tree, optionally nominate a diary workspace |
| `firehose` | Route a mixed dump into events vs tasks |
| `create-event`, `edit-event`, `delete-event`, `batch-create-events` | Calendar CRUD |
| `create-task`, `edit-task`, `delete-task`, `batch-create-tasks` | Todoist CRUD |
| `task-to-event`, `event-to-task` | Two-part migration between services |
| `review-missing-priorities`, `assign-priorities` | Todoist priority hygiene |
| `review-missing-dates`, `assign-dates` | Todoist date hygiene |
| `agenda` | Meeting agenda Doc lifecycle (sub-actions: `create`, `link`, `share`, `email`) |
| `minutes` | Meeting minutes Doc lifecycle (sub-actions: `capture`, `share`, `email`) |
| `wrapup` | EOD/EOW/period summary Doc with achievements + open items |
| `morning-brief` | Resume from last wrapup + today's calendar/tasks |
| `log-entry` | Markdown diary entry (only if diary workspace nominated) |
| `setup-automation` | Stub: outlines options for scheduling `wrapup` and `morning-brief` |

## State

Plugin config lives at `${CLAUDE_USER_DATA:-${XDG_DATA_HOME:-$HOME/.local/share}/claude-plugins}/schedule-manager/config.json`.

The plugin **does not** write user content (diary entries, agendas, minutes, wrapups) under `$CLAUDE_USER_DATA`. Drive content lives in the user's Drive; diary markdown lives in a folder the user nominates during onboarding.

## Installation

```bash
claude plugins install schedule-manager@danielrosehill
```

After installation, run the `onboard` skill before using anything else.

## License

MIT

---
name: log-entry
description: Write a dated diary entry as a markdown file in the user's nominated diary workspace. Requires diary.enabled in config.
---

# Log Diary Entry

Writes one markdown file per entry to the user's nominated diary path. **Local-only**; never uploaded to Drive. Skill is dormant until the diary workspace is set up via `onboard`.

## Steps

1. **Read config.** If `diary.enabled` is false or `diary.path` is null, tell the user to run `onboard` and enable diary support, then stop.

2. **Determine entry date.** Default today (per `config.defaults.timezone`); allow user override.

3. **Determine filename.** `YYYY-MM-DD.md`. If a file for that date exists, ask whether to append or overwrite.

4. **Capture the entry body.** Either the user already provided it, or prompt for it.

5. **Write file** with frontmatter:
   ```yaml
   ---
   date: YYYY-MM-DD
   tags: []
   mood: ""
   ---
   ```

6. **Confirm path written.** Do not echo the entry body back.

## Notes

- The diary directory may live anywhere on the user's filesystem (synced via Dropbox/Drive desktop sync, a git repo, etc.) — the plugin doesn't care.
- No content goes to `$CLAUDE_USER_DATA`. Only the pointer.

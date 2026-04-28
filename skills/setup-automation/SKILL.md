---
name: setup-automation
description: Stub — set up automatic recurring runs of wrapup and morning-brief via the user's preferred scheduler. Currently outlines options without configuring.
---

# Setup Automation (stub)

This skill is a placeholder until tooling preferences are gathered. It documents the options and lets the user pick one to implement.

## Options to surface

When invoked, walk the user through these choices:

1. **systemd user timer** — Linux native, no extra deps. Two unit files per cadence (timer + service).
2. **cron** — universal, simple, less observable.
3. **KDE / GNOME scheduled task** — desktop-integrated, fragile across reboots.
4. **n8n workflow** — if the user runs n8n. Cron node → exec node calling Claude Code in headless mode.
5. **Home Assistant automation** — if the user runs HA. Time trigger → shell_command service.
6. **Claude Code's native scheduling** — `/schedule` for one-time or recurring agent runs (cloud).

## What NOT to do yet

- Don't write systemd units or cron entries from this skill. Once the user picks an approach, scaffold the implementation in a follow-up (or hand off to the relevant plugin: `homelab-private` for HA/systemd, etc.).

## Suggested cadence

- `morning-brief` — weekday mornings, 07:00 local
- `wrapup` — weekday evenings, 18:00 local; weekly variant Friday 17:00

Confirm cadence with the user before any future implementation step.

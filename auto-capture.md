---
title: Auto-Capture (Make It Automatic)
nav_order: 6
---

PastChats Memory is **not** an MCP that automatically intercepts your chat messages.

Right now it works like this:

1. Your chat tool (Claude Code / exports / logs) writes conversations somewhere on disk.
2. You run `pastchats-memory index` to pull those files into SQLite.
3. You run `pastchats-memory recall` before a new task.

The “automatic” part comes from **automating the index command**.

## Option A (recommended): Re-index on a schedule

This is the simplest and most reliable approach.

### macOS/Linux (cron)

Open your crontab:

```bash
crontab -e
```

Add a line (runs every 30 minutes):

```cron
*/30 * * * * cd /path/to/pastchats-memory && . .venv/bin/activate && pastchats-memory index --db .swarm/prompt_memory.db --input /path/to/your/chat_logs >/tmp/pastchats-index.log 2>&1
```

What you change:

- `/path/to/pastchats-memory` = where you cloned the repo
- `/path/to/your/chat_logs` = folder that contains your chat exports/logs

### Windows

Use Task Scheduler to run the same command (or run it inside WSL).

## Option B: Watch a folder and index on change

If your chat tool writes new files continuously to one folder, you can trigger indexing when something changes.

This is more fragile than scheduling, but feels “live”.

Recommended workflow:

- Pick a single folder where new logs land
- Watch that folder
- Run index when files change

If you want this, open an issue and say your OS + where your tool stores logs. We can add a supported watcher script.

## Option C: “MCP memory server” (what that would mean)

An MCP server can expose tools like:

- `recall(query)` (returns memory blocks)
- `index_text(text, metadata)` (store new turns as you work)

But MCP does not magically capture chats by itself.

Something still has to call `index_text(...)` or write files that you index.

If you want this project to become a true MCP “always-on memory”, we can add:

1. An MCP server wrapper around the existing DB
2. A small “logger” integration that sends each new turn to the server

## Quick sanity check

If you think it’s auto-capturing but it isn’t, run:

```bash
pastchats-memory stats --db .swarm/prompt_memory.db
```

If prompt count isn’t increasing over time, your index automation isn’t pointed at the right folder.


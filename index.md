---
title: Home
nav_order: 1
description: What this is and why you should use it.
---

If you use AI coding assistants, you probably repeat the same mistakes across projects.

PastChats Memory fixes that by giving your agent **long-term memory**:

1. It indexes your old conversation history.
2. It stores keyword index + vectors in SQLite.
3. Before a new task, it recalls what worked and what failed.

## What “memory” looks like (example)

You run:

```bash
pastchats-memory recall --db .swarm/prompt_memory.db --query "webhook retry idempotent"
```

You get:

```text
# Memory Recall
Query: webhook retry idempotent

## Memory 1 [0.190] - my_project
Prompt: build retries with idempotency keys
What worked: use bounded exponential backoff and store idempotency key state
Source: /path/to/chat.md (turn 0)
```

This is designed to be pasted into your agent context before coding.

## Why use it

- Fewer repeated mistakes
- Faster starts on new tasks
- Reuse proven patterns from old projects
- Keep memory local (SQLite file)

## What it does under the hood

- **Lexical search:** FTS5 (fast keyword matching)
- **Semantic search:** vector similarity (sqlite-vec when available)
- **Hybrid rank:** combines both signals
- **Recall mode:** prints practical "what worked" context with sources

## Start in 5 minutes

1. Copy/paste the [Vibe Coder Cheat Sheet](cheat-sheet.md)
2. Run the exact commands in [Quick Start](getting-started.md)
3. Use [Search & Recall](search-and-recall.md)
4. Read [How It Remembers (Simple)](how-it-remembers.md)

## Next: common patterns

If you like recipes, go straight to [Common Workflows](workflows.md).

## Who this is for

- Solo builders
- Teams using Claude Code / coding agents
- "Vibe coders" who want practical defaults and copy-paste commands

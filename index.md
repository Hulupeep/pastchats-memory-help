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

1. Open [Installation](installation.md)
2. Run the exact commands in [Quick Start](getting-started.md)
3. Use [Search & Recall](search-and-recall.md)

## Who this is for

- Solo builders
- Teams using Claude Code / coding agents
- "Vibe coders" who want practical defaults and copy-paste commands

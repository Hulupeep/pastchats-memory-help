---
title: Quick Start
nav_order: 2
---

# Quick Start

Use this if you want the shortest path.

## 1. Install

```bash
git clone https://github.com/Hulupeep/pastchats-memory.git
cd pastchats-memory
python3 -m venv .venv
source .venv/bin/activate
pip install -e .[dev]
```

## 2. Initialize memory DB

```bash
pastchats-memory init --db .swarm/prompt_memory.db
```

## 3. Index your chat history

```bash
pastchats-memory index --db .swarm/prompt_memory.db --input ~/projects
```

You can pass multiple paths:

```bash
pastchats-memory index --db .swarm/prompt_memory.db --input ~/projects ~/Downloads/chat_exports
```

## 4. Recall before coding

```bash
pastchats-memory recall --db .swarm/prompt_memory.db --query "idempotent webhook retry strategy"
```

## 5. Use that output as context for your new task

That’s it.

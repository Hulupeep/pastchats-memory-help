---
title: Vibe Coder Cheat Sheet
nav_order: 2
---

If you only read one page, read this.

## Install

```bash
git clone https://github.com/Hulupeep/pastchats-memory.git
cd pastchats-memory
python3 -m venv .venv
source .venv/bin/activate
pip install -e .
```

## Create the memory DB

```bash
pastchats-memory init --db .swarm/prompt_memory.db
```

## Index your history

Point this at whatever folder(s) contain your chat exports or coding-agent logs.

```bash
pastchats-memory index --db .swarm/prompt_memory.db --input ~/projects
```

Index multiple places:

```bash
pastchats-memory index --db .swarm/prompt_memory.db --input ~/projects ~/Downloads/chat_exports
```

Only index user+assistant:

```bash
pastchats-memory index --db .swarm/prompt_memory.db --input ~/projects --roles user,assistant
```

## Recall before you code

Write your query like:

`<problem> + <constraint> + <stack>`

Example:

```bash
pastchats-memory recall --db .swarm/prompt_memory.db --query "webhook retry idempotent python"
```

## If recall is empty

Do this:

- Make the query more specific (include stack + constraint)
- Index more history
- Proceed normally (don’t force it)

## Optional speed boost (sqlite-vec)

If you installed sqlite-vec:

```bash
export PROMPT_MEMORY_SQLITE_VEC_PATH=/absolute/path/to/vec0.so
```

Then re-run `index`.

## Optional better semantic search (OpenAI embeddings)

```bash
pip install -e .[openai]
export OPENAI_API_KEY=your_key
pastchats-memory index --db .swarm/prompt_memory.db --input ~/projects --embed-provider openai
```

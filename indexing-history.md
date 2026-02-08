---
title: Indexing History
nav_order: 5
---

## Supported file types

- `.json`
- `.jsonl`
- `.md` / `.markdown`
- `.txt`

## Basic indexing

```bash
pastchats-memory index --db .swarm/prompt_memory.db --input ~/projects
```

## Role filtering

Only keep user + assistant turns:

```bash
pastchats-memory index \
  --db .swarm/prompt_memory.db \
  --input ~/projects \
  --roles user,assistant
```

## Re-indexing is safe

The system deduplicates by content hash, so re-running index is normal.

## Best practice

- Run indexing once a day (or after big work sessions)
- Index only folders that actually contain chat exports/history
- Keep one DB per personal workflow unless you need strict separation

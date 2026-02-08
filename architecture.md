---
title: Architecture
nav_order: 11
---

# Architecture

## Components

- `parsers.py` parses raw history files into normalized turns.
- `store.py` owns SQLite schema, writes, and retrieval.
- `embeddings.py` provides local hash or OpenAI embedding providers.
- `search.py` merges lexical + semantic rankings.
- `cli.py` exposes `init`, `index`, `search`, `recall`, `stats`.

## Storage model

- `prompts` table: normalized turns + metadata
- `prompts_fts` virtual table: FTS5 index for keyword matching
- `prompt_embeddings` table: serialized vectors
- `index_runs` table: indexing run audit trail

## Retrieval model

1. Lexical candidate set via FTS5
2. Semantic candidate set via sqlite-vec or fallback cosine
3. Weighted hybrid score merge
4. `recall` format adds next assistant turn as "What worked"

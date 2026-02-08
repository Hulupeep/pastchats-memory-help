---
title: Troubleshooting
nav_order: 13
---

## "command not found: pastchats-memory"

Activate your virtualenv first:

```bash
source .venv/bin/activate
```

Then reinstall editable package:

```bash
pip install -e .
```

## `sqlite_vec_loaded` is false

Not a blocker. Fallback search still works.

If you want sqlite-vec:

1. Install extension
2. Set `PROMPT_MEMORY_SQLITE_VEC_PATH`
3. Re-run `init` or `index`

## Index says `prompts_indexed: 0`

Possible reasons:

- You indexed same files before (dedupe)
- Folder has no supported history files
- Parser did not find role/content format

Try a specific known file first:

```bash
pastchats-memory index --db .swarm/prompt_memory.db --input /path/to/one_chat.md
```

## Search returns weak results

- Improve query specificity
- Re-index more history
- Include role filters when indexing
- Use OpenAI embeddings for better semantic quality

## OpenAI embedding errors

Check:

```bash
echo $OPENAI_API_KEY
pip show openai
```

Then rerun with `--embed-provider openai`.

---
title: sqlite-vec Setup
nav_order: 14
---

PastChats Memory works without `sqlite-vec`, but it is faster at scale when enabled.

## 1. Install sqlite-vec

Use the official install method for your OS from the sqlite-vec project.

## 2. Point the app to the extension

```bash
export PROMPT_MEMORY_SQLITE_VEC_PATH=/absolute/path/to/vec0.so
```

## 3. Verify during init/index

You should see:

- `"sqlite_vec_loaded": true`

If false, fallback cosine search is used.

## Notes

- Fallback mode is expected and supported.
- You can ship to teammates without forcing sqlite-vec setup.

---
title: Installation
nav_order: 4
---

## Requirements

- Python 3.10+
- macOS/Linux/WSL
- Your chat history files (JSON, JSONL, MD, TXT)

## Base install

What you are installing:

- A small Python command-line tool named `pastchats-memory`
- It runs locally on your machine
- It does not upload your chats anywhere by default
- It uses a local SQLite database file (you choose the path)
- It can print “memory recall” blocks that include what you asked + what worked + where it came from

What you are not installing (yet):

- sqlite-vec (optional acceleration)
- OpenAI embeddings (optional)

```bash
git clone https://github.com/Hulupeep/pastchats-memory.git
cd pastchats-memory
python3 -m venv .venv
source .venv/bin/activate
pip install -e .
```

`pip install -e .` means:

- Install this repo as a Python package into the virtualenv
- Add the `pastchats-memory` command
- “Editable” means if you update the code, you do not need to reinstall

## Optional extras

### Run tests

```bash
pip install -e .[dev]
pytest
```

### OpenAI embedding provider

```bash
pip install -e .[openai]
export OPENAI_API_KEY=your_key
```

### sqlite-vec acceleration

What sqlite-vec is (in normal words):

- Semantic search uses “vectors” (a list of numbers per prompt)
- If you have a lot of history, comparing vectors can get slow
- `sqlite-vec` is a SQLite extension that makes vector search fast

You do not need it to start. Everything still works without it.

When you do want it:

- You indexed thousands of prompts and recall feels slow
- You want faster semantic retrieval

After you install the extension, you point PastChats Memory at the file:

```bash
export PROMPT_MEMORY_SQLITE_VEC_PATH=/absolute/path/to/vec0.so
```

If not set, PastChats Memory still works using fallback cosine search.

If you do not know the path yet, follow the “sqlite-vec Setup” page.

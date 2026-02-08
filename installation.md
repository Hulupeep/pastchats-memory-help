---
title: Installation
nav_order: 3
---

# Installation

## Requirements

- Python 3.10+
- macOS/Linux/WSL
- Your chat history files (JSON, JSONL, MD, TXT)

## Base install

```bash
git clone https://github.com/Hulupeep/pastchats-memory.git
cd pastchats-memory
python3 -m venv .venv
source .venv/bin/activate
pip install -e .
```

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

Install `sqlite-vec` then set:

```bash
export PROMPT_MEMORY_SQLITE_VEC_PATH=/path/to/vec0.so
```

If not set, PastChats Memory still works using fallback cosine search.

---
title: How It Remembers (Simple)
nav_order: 7
---

This tool does not “magically learn your brain”. It does something simpler and more reliable:

1. You point it at chat history files.
2. It saves those conversations into a local database.
3. Later, you ask a question and it finds the most similar past moments.
4. It prints those moments in a readable way before you start coding.

## What gets captured

PastChats Memory captures the text of your past conversations as **turns**:

- `user`: what you asked
- `assistant`: what the AI answered

It also keeps basic metadata so results are trustworthy:

- which file it came from
- which “project” it came from (inferred from folder)
- which turn number inside the conversation

You control what it captures by choosing what to index:

```bash
pastchats-memory index --db .swarm/prompt_memory.db --input ~/projects
```

If it’s not in the indexed folders, it won’t be remembered.

## Does it auto-log my chats?

Not by itself.

PastChats Memory does **not** intercept chat messages. It only indexes files you point it at.

To make it automatic, set up scheduled indexing (see: [Auto-Capture](auto-capture.md)).

## How it becomes searchable

It builds two ways to search the same text:

1. Keyword search (fast, exact-ish)
2. “Meaning” search (find similar ideas even if the words differ)

Then it combines both into one final ranking.

You don’t need to understand the math. You just write better queries:

`<problem> + <constraint> + <stack>`

Example:

`webhook retry idempotent python`

## Why recall output is readable

`recall` is designed to be copy-paste context for an agent.

When it finds a past `user` prompt that looks relevant, it also grabs the next `assistant` reply and labels it:

- `Prompt:` (what you asked back then)
- `What worked:` (the answer you got back then)
- `Source:` (where it came from)

### Example output

```text
# Memory Recall
Query: retry strategy

## Memory 1 [0.190] - my_project
Prompt: build retries with idempotency keys
What worked: use bounded exponential backoff and store idempotency key state
Source: /path/to/chat.md (turn 0)
```

This is the “long-term memory” effect: it keeps you from re-learning the same lesson repeatedly.

## What it does not do

- It does not update an LLM’s training.
- It does not guarantee the retrieved answer is correct.
- It does not auto-capture new chats unless you index them.

Think of it like: “grep + semantic search across your past AI work, with clean output.”

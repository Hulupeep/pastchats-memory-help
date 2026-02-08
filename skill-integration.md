---
title: Agent Skill Integration
nav_order: 13
---

PastChats Memory includes a reusable skill:

- `skills/prompt-memory-recall/SKILL.md`

## Goal

Force a memory lookup before implementation starts.

## What this is (plain English)

- The “skill” is instructions for your agent to run `recall` before it starts coding.
- It does not automatically log chats.
- It makes “check memory first” the default behavior.

## Simple pattern

1. Receive new task
2. Generate short recall query
3. Run recall command
4. Inject top lessons into planning context
5. Start coding

## Script helper

```bash
skills/prompt-memory-recall/scripts/pre_task_recall.sh "idempotent retries node"
```

## Minimal injected context format

```text
Memory lessons:
1) Use idempotency keys at write boundary (source: ...)
2) Avoid blind retries on 4xx (source: ...)
3) Add bounded exponential backoff (source: ...)
```

Keep it short. Use memory to guide, not to overfit.

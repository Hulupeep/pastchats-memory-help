---
title: Workflow While You Work
nav_order: 7
---

The purpose is simple: **stop repeating yourself**.

You already solved things in past chats. This makes those solutions show up at the right moment, without scrolling old threads.

## Where the value comes from

Past chats contain:

- decisions you already made (tradeoffs)
- failure modes you already hit
- commands/configs that actually worked
- project-specific context (paths, tools, conventions)

The value is highest:

- at the start of a task (planning)
- when stuck on a recurring error
- before refactors/migrations (avoid regressions)

## Recommended workflow (fast + low friction)

### 1) Keep the DB up to date (background)

You have two choices:

- Manual: re-run `index` when you remember
- Automatic: run `index` on a schedule (recommended)

The important part: indexing is not “every second”. It’s periodic.

### 2) Before a new task (the main event)

Run recall once:

```bash
pastchats-memory recall --db .swarm/prompt_memory.db --query "<intent>" --limit 5
```

Then inject the top 1-3 lessons into your plan.

This is the core loop.

### 3) When debugging

Use `search` with the actual error message:

```bash
pastchats-memory search --db .swarm/prompt_memory.db --query "<error> <library>" --limit 10
```

### 4) After you finish (optional)

If your chat tool writes new logs to disk, run `index` again so the DB learns from the new session.

## Is this a hook? an MCP? a skill?

### Skill

A skill is just instructions that tell your agent:

- when to run recall
- how to format the results

This repo includes a skill that does exactly that.

### Hook

A hook is automation inside your agent runner (if your tool supports it).

Best hook behavior:

- pre-task hook: run recall once per task
- post-task hook: run index (optional)

### MCP

An MCP server would expose tools like `recall(query)`.

It does not automatically capture chats unless something calls “store”.

If you want a true “always-on memory”, you need:

- an MCP server, plus
- a logger integration that sends each new turn into it

## How to avoid slowing things down

- Do not run `index` continuously. Run it on a schedule.
- Keep recall small: `--limit 3` to `--limit 5`.
- Use local embeddings (default) for zero network latency.
- Only enable sqlite-vec when you have enough data that semantic search feels slow.

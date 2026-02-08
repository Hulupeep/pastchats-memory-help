---
title: Common Workflows
nav_order: 12
---

Copy/paste these queries and patterns.

## Workflow: Start any task

1. Convert the task into a short intent query.
2. Run recall.
3. Use the top 1-3 lessons.

```bash
pastchats-memory recall --db .swarm/prompt_memory.db --query "<intent>" --limit 5
```

Good intent query format:

`<feature> <constraint> <stack> <integration>`

Example:

`payments webhook retry idempotent node stripe`

## Workflow: Debug a recurring error

Use the actual error message (or part of it).

```bash
pastchats-memory search --db .swarm/prompt_memory.db --query "<error message> <library>" --limit 10
```

Then:

- Apply the smallest safe fix first.
- If you change behavior, add a test.

## Workflow: Migrations and schema changes

```bash
pastchats-memory recall --db .swarm/prompt_memory.db --query "sqlite migration backwards compatible rollback" --limit 5
```

What to look for in memory:

- rollback strategy
- data backfill patterns
- safe defaults

## Workflow: Refactors

```bash
pastchats-memory recall --db .swarm/prompt_memory.db --query "refactor <component> contract tests regressions" --limit 5
```

What to do with results:

- list invariants you must not break
- do changes in small commits
- keep behavior stable

## Workflow: Performance work

```bash
pastchats-memory recall --db .swarm/prompt_memory.db --query "optimize <thing> profiling p95" --limit 5
```

## Workflow: New repo bootstrap

```bash
pastchats-memory recall --db .swarm/prompt_memory.db --query "project scaffolding packaging ci tests" --limit 5
```

## Workflow: “I don’t know what to search for”

Start with one of these:

- `"how to" + <tool> + <your goal>`
- `<domain> + "pitfalls" + <stack>`
- `<feature> + "edge cases"`

Then refine.

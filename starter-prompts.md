---
title: Starter Prompts (Claude Code)
nav_order: 6
---

Copy-paste these.

## 1) Default: recall before coding

```text
Before you start, run PastChats Memory recall.

- Derive a short intent query from my request.
- Run:
  pastchats-memory recall --db .swarm/prompt_memory.db --query "<intent>" --limit 5
- Summarize the top lessons as:
  Memory lessons:
  1) ... (source: ...)
  2) ... (source: ...)
  3) ... (source: ...)

Then proceed with implementation.
```

## 2) If memory is empty or low quality

```text
If recall returns weak results, say "No strong prior memory found" and proceed normally.
Do not invent details.
```

## 3) When debugging a recurring failure

```text
Search memory specifically for prior failures and fixes.

Run:
  pastchats-memory search --db .swarm/prompt_memory.db --query "<error message> <component>" --limit 10

Then:
- Identify 1-3 matching past fixes
- Apply the smallest safe change first
- Cite the source file/turn you used
```

## 4) When doing refactors

```text
Before refactoring, run recall for:
  "refactor <component> regression tests contract".

Then:
- List known invariants/contract tests to preserve
- Propose a refactor plan with checkpoints
- Keep changes small and verifiable
```

## 5) When starting a brand-new repo

```text
Before building anything, run recall for:
  "project scaffolding mistakes packaging ci".

Then:
- Use the top lessons to pick the initial stack
- Add minimal CI + tests early
```

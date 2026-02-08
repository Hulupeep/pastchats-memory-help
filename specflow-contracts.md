---
title: SpecFlow Compliance
nav_order: 9
---

# SpecFlow Compliance

This project ships with SpecFlow-style contracts and stories.

## Contract files

- `docs/contracts/feature_architecture.yml`
- `docs/contracts/feature_prompt_memory.yml`
- `docs/contracts/journey_pre_task_recall.yml`
- `docs/contracts/CONTRACT_INDEX.yml`

## Story files

- `docs/stories/EPIC-001-prompt-memory.md`
- `docs/stories/STORY-001-index-and-recall.md`

## What these enforce

- Architecture invariants (layering, FTS5, recall command)
- Memory invariants (embedding parity, hybrid ranking, fallback behavior)
- Journey definition for pre-task recall flow

## Run contract tests

```bash
pytest tests/contracts
```

If a contract fails, fix the implementation first, then update contracts only when requirements truly change.

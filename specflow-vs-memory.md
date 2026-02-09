---
title: Specflow vs Memory (What’s Different)
nav_order: 15
---

They solve different problems and work best together.

## One-line summary

- **Specflow:** makes requirements enforceable (contracts that fail builds when violated).
- **PastChats Memory:** makes experience reusable (recall what worked/failed before you start).

## Comparison

| Dimension | Specflow | PastChats Memory |
|---|---|---|
| Primary purpose | Prevent violations of invariants | Prevent repeated mistakes |
| Output | Contract YAML + tests + journeys | Recall blocks + search hits |
| Behavior | Deterministic gate (pass/fail) | Advisory context (ranked suggestions) |
| When it runs | CI / test time | Pre-task (and during debugging) |
| What it “knows” | Your explicit requirements | Your historical chats and fixes |
| Failure mode | Blocks merges when rule violated | Can retrieve irrelevant/dated memory |
| Maintenance cost | Keep contracts/tests updated as requirements change | Keep indexing pipeline pointed at real logs |

## How they fit together (recommended)

1. Use **Specflow** to define invariants and journeys for the feature.
2. Use **PastChats Memory recall** before implementing to pull up prior patterns/pitfalls.
3. Implement.
4. Specflow contract tests catch violations during verification.
5. Store new turns so the next task starts smarter.

## Practical rule

If you need to know what MUST stay true: Specflow.

If you need to remember what worked last time: Memory.

---
title: Search and Recall
nav_order: 5
---

## Search (debug / exploration)

```bash
pastchats-memory search --db .swarm/prompt_memory.db --query "graphql pagination cursor"
```

This returns ranked hits with score + source file + turn index.

## Recall (for task startup)

```bash
pastchats-memory recall --db .swarm/prompt_memory.db --query "safe database migration rollback"
```

This prints a compact memory block you can use directly in your agent context.

## Query writing tips

Use this pattern:

`<problem> + <constraint> + <stack>`

Examples:

- `webhook retry idempotent python`
- `react form validation zod edge cases`
- `sqlite migration backwards compatible`

## JSON output mode

```bash
pastchats-memory recall --db .swarm/prompt_memory.db --query "auth middleware" --json
```

Useful for scripting or tool integrations.

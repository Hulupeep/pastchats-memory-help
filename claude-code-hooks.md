---
title: Claude Code Hooks Setup
nav_order: 8
---

This is the "make it automatic" setup for Claude Code.

You will get:

- automatic memory recall injected when you submit a prompt
- automatic capture of Claude's final answer into your memory DB

## How it works

Claude Code hooks run a command and pass JSON on stdin.

- `UserPromptSubmit` hook:
  - stores your prompt into the memory DB
  - prints a short "Memory lessons" block to stdout
  - Claude Code injects that stdout into context (so Claude sees it before responding)

- `Stop` hook:
  - reads the transcript file
  - stores the latest assistant response into the memory DB
  - prints nothing

## 0) Install `pastchats-memory` so hooks can run it

Hooks need `pastchats-memory` available in your PATH.

### Option A (recommended): pipx install (global command)

```bash
pipx install git+https://github.com/Hulupeep/pastchats-memory.git
```

### Option B: use a repo checkout + venv

Clone once:

```bash
git clone https://github.com/Hulupeep/pastchats-memory.git ~/pastchats-memory
cd ~/pastchats-memory
python3 -m venv .venv
source .venv/bin/activate
pip install -e .
```

Then reference the full path to the binary in your hook command.

## 1) Create your memory DB

Pick one global DB path. Example:

```bash
pastchats-memory init --db ~/.claude/prompt_memory.db
```

## 2) Configure hooks

Edit your Claude Code settings file.

- user-level: `~/.claude/settings.json`
- project-level: `.claude/settings.json`

Add:

```json
{
  "hooks": {
    "UserPromptSubmit": [
      {
        "hooks": [
          {
            "type": "command",
            "command": "pastchats-memory hook-user-prompt-submit --db ~/.claude/prompt_memory.db --limit 3"
          }
        ]
      }
    ],
    "Stop": [
      {
        "hooks": [
          {
            "type": "command",
            "command": "pastchats-memory hook-stop --db ~/.claude/prompt_memory.db"
          }
        ]
      }
    ]
  }
}
```

## 3) Verify

1. Start a new Claude Code session.
2. Submit a prompt.
3. You should see a short injected block starting with:

`Memory lessons (from past chats):`

## Performance notes (so it doesn't slow you down)

- This runs recall once per prompt submit, and stores one row per stop.
- Use local embeddings (default) for offline speed.
- Keep `--limit 3`.
- If you have a huge DB and it feels slow, enable sqlite-vec later.

## If you want true MCP usage

You can run the MCP server (`pastchats-memory-mcp`) and have Claude call `recall()` as a tool.

For hooks, the CLI approach above is simpler and faster.

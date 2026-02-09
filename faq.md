---
title: FAQ
nav_order: 18
---

## Is this cloud memory?

No. Default setup is local SQLite on your machine.

## Do I need sqlite-vec?

No. It is optional acceleration.

## Can I index multiple projects?

Yes. Pass multiple paths to `--input`.

## Can I run this before every task automatically?

Yes. Use the included skill and helper script to run recall in your task-start workflow.

## Is this only for Claude?

No. Any agent or script that can execute CLI commands can use it.

## Can I keep separate memory DBs?

Yes. Use different `--db` paths per client/team/domain.

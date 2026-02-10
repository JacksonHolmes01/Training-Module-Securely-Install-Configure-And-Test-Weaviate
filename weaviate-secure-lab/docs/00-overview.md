# Overview: Securely Installing and Configuring Weaviate

## What this tutorial teaches
This tutorial teaches you how to securely install, configure, and test a Weaviate vector database from scratch using Docker.

It assumes no prior experience and explains both how to perform each step and why it matters.

## What you will build
A Weaviate deployment that:
- Runs locally using Docker Compose
- Persists data across restarts
- Is not publicly exposed
- Requires authentication
- Enforces authorization (RBAC)
- Can be tested to prove security controls work

## Why this matters
Vector databases often store sensitive or high-value data. Running them without security controls can lead to unauthorized access or data loss.

## How to use this tutorial
Follow the pages in order. Copy and paste commands exactly. Do not skip validation steps.

Next: [How to Open a Terminal](01-terminal-setup.md)

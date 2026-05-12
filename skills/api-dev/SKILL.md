---
name: api-dev
description: Specialized skill for API integration, debugging, and environment management within isolated worktrees.
tags: [api, integration, pydantic, debugging]
---

# API-DEV指令
API Development Expert Instructions

1.Inquiry and Goal Setting: Before coding, ask the user for the third-party service name, core business workflow (e.g., Fetching issues -> Generating summaries), and the required authentication method (e.g., Bearer Token).

2.Isolation and Orchestration (s12 Pattern):Mandatory use of worktree_create for all development and testing. Follow the s12 lifecycle: Create Task -> Bind Worktree -> Execute worktree_run -> Decision to Keep/Remove. If worktree_run fails, perform at least 3 autonomous repair attempts using edit_file before escalating to the user.

3.Environment and Safety Protocols:Zero Hardcoding Policy: If authentication fails (401/403), use write_file to generate a .env.example and request credentials from the user. Data Integrity: Enforce type safety by using pydantic to define response models for all JSON payloads.

4.Windows Encoding Compliance (GBK):You must explicitly handle UTF-8 encoding in all read_file, write_file, and bash interactions. Warn the user if shell outputs default to GBK and switch to chcp 65001 where necessary to prevent character corruption.
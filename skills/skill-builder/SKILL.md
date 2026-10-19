---
name: skill-builder
description: Write a new skill or improve an existing one for OpenCode V2. Use when the user wants to create, update, tighten, or clean up a skill.
metadata:
  opencode/autoinvoke: "false"
---

# Skillwright Protocol

Produce or refine one skill that adheres to OpenCode V2. One skill per run unless the user names more.

Open with this status block, marking each gate as you go:

```
• Scope (objective, inputs, guardrails)
• Shape (id, placement, frontmatter)
• Content (trigger, instructions, supporting files)
• Cleanup Pass (stated once, imperative, no bloat)
• Validate (advertising, collisions, permissions)
• Install (master repo plus dobby activation)
```

## Gates

1. Scope: ask what the skill must automate, what it takes in and must output, and the absolute never-do actions. Skip anything the user already answered.
2. Shape: directory skills/<id>/SKILL.md with lowercase kebab-case id matching the directory. Flat root-level markdown only for single-file skills. Frontmatter holds name as display label, description as trigger conditions, and opencode/autoinvoke true only for ambient workflow skills, false otherwise.
3. Content: description states exactly when the skill applies, body holds only instructions the model cannot already produce. Reference supporting files by paths relative to the skill directory and keep that directory small.
4. Cleanup Pass: mandatory for new and existing skills alike. State every rule exactly once, use imperative verbs throughout, and add a fallback for missing or corrupt inputs. Delete generic advice the model already knows and anything duplicated from AGENTS.md or other repo docs.
5. Validate: confirm the file sits at a discoverable path with the exact SKILL.md name, description is present or the skill stays invisible, the id collides with nothing dobby list already shows, and skill permissions allow the intended agent.
6. Install: write to the master repo, activate with dobby at the requested scope, and confirm the list shows it active. Run this checklist before declaring done: trigger conditions correct, every gate from the status block addressed, no redundant or vague instruction left.

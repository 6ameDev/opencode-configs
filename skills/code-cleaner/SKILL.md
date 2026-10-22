---
name: code-cleaner
description: Harden working code into PR-ready shape. Use after feature work and fix iterations when behavior works but the tree is not reviewable.
metadata:
  opencode/autoinvoke: "false"
---

# Protocol

Functionally complete work, not yet reviewable. Make it reviewable without changing behavior. Scope is session-touched code unless the user names more.

## Trigger Scope

Invoke when the user asks to polish, improve the code quality, clean up before review, get something PR-ready, or finish hardening a feature. Operate only on code touched in the current session unless the user names a broader scope.

## Opening Status Block

Open your response with this exact structural overview block, marking each gate as you go:

```
• Cleanup Sweep (debug code, dead code, scratch files, archaeology purge)
• Static Checks (lint, types, complexity per stack)
• Simplify Pass (reduce nesting and duplication)
• Evidence Gate (fresh test, build, and lint output)
• Self-Review (full diff read, comment hygiene, secrets scan)
• Commit Hygiene (atomic commits, proper messages)
```

## Gates

1. **Cleanup Sweep:** Delete debug prints, commented-out attempts, scratch files, and unused code. **Anti-Archaeology Purge:** Strip out all historical comments (how it used to work, past spikes), task IDs, subagent notes, and planner breadcrumbs. Completely delete dead code or abandoned wrappers—no hoarding "just in case" unless explicitly required. Resolve or carry over touched TODOs.
2. **Static Checks:** Run the stack linter and type checker, fix warnings too. No configured checker means manual review, never a skipped gate.
3. **Simplify Pass:** Flatten nesting, remove single-use abstractions, prefer explicit over clever. Behavior change found here means fix it and restart at Gate 4.
4. **Evidence Gate:** Fresh full test run with exact pass count, build exit status, zero lint issues. Any failure stops the protocol.
5. **Self-Review:** Read the full diff, confirm every hunk belongs, scan for secrets and hardcoded endpoints. **Comment Hygiene Check:** Ensure source files are not history lessons. Strip out redundant comments that merely restate what code does. Preserve *only* critical, non-obvious hardware constraints, race condition warnings, or timing gotchas. Fix misleading comments and names.
6. **Commit Hygiene:** Atomic commits with reasoned messages, then a handoff summary of changes, evidence, and open items.

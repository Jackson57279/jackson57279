Selected skills: read-only-explorer, requirements-to-task-packet
Skill paths passed to child Pi: 2

# Applicable Skills
The following skills were selected for this worker. Follow them when they match the current task. If a selected skill conflicts with the explicit task packet, project AGENTS.md, or user request, follow the stricter/higher-priority instruction and report the conflict.

## read-only-explorer
Description: Read-only exploration and audit workflow. Use for explorer, analyst, reviewer, and source-audit roles that must inspect code without modifying files.
Source: package:skills/read-only-explorer

# read-only-explorer

Use this skill for explorer, analyst, reviewer, and source-audit roles. These roles must inspect code without modifying it.

## Core Contract

1. **Do not edit files** — no write, no edit, no delete
2. **Do not write generated artifacts** outside the run artifact directory
3. **Prefer read-only commands**: `read`, `rg`, `find`, `ls`, `git status`
4. **Record exact files inspected** — include path and relevant line numbers
5. **Distinguish direct evidence from inference** — don't guess
6. **If implementation is needed, recommend** — don't modify code

## Tool Selection Guide

Choosing the right tool for the task reduces noise and speeds up discovery.

### `rg` (ripgrep) — Code pattern search

**Best for:** Finding function definitions, imports, patterns, usages
```
# Find all uses of a function
rg "functionName" --type ts

# Find with context (2 lines before/after)
rg "pattern" -B2 -A2

# Case-insensitive
rg -i "error handling"

# Only match whole word
rg -w "agent"

# JSON output for machine parsing
rg "pattern" --json | head -20

# Respect .gitignore (skip node_modules)
rg "pattern" --type-add 'exclude:*.json' --type ts
```

### `find` — File and directory search

**Best for:** Finding files by name, type, or path pattern
```
# Find all TypeScript files
find . -name "*.ts" -not -path "*/node_modules/*" | head -20

# Find recently modified files
find . -name "*.ts" -mtime -7 | head -20

# Find files larger than 100

[skill instructions truncated]

---

## requirements-to-task-packet
Description: Use when a goal, issue, roadmap item, review finding, or user request must become actionable worker tasks.
Source: package:skills/requirements-to-task-packet

# requirements-to-task-packet

Core principle: workers need explicit task packets, not inherited ambiguity. Ask only when ambiguity changes architecture, safety, public behavior, or data loss risk; otherwise record assumptions.

Distilled from detailed reads of clarification, spec-to-implementation, subagent-driven development, and skill-authoring patterns.

## Clarify or Proceed

Ask before implementation when ambiguity affects:

- security boundary, permissions, ownership, or secret handling;
- destructive operations, migrations, publishing, or public API behavior;
- architecture or data model;
- acceptance criteria or rollback expectations.

Proceed with explicit assumptions when ambiguity is local, reversible, and testable.

## Task Packet Template

```text
Objective:
Scope/paths:
Allowed edits:
Forbidden edits/non-goals:
Inputs/dependencies:
Relevant context/artifacts:
Assumptions:
Risks:
Acceptance criteria:
Verification commands:
Expected output artifacts:
Escalation conditions:
```

## Subagent Context Rules

- Give each worker fresh, curated context; do not rely on hidden parent history.
- Include exact upstream artifact paths and summaries when needed.
- Keep implementation tasks independent or explicitly sequenced.
- Require workers to report one of: DONE, DONE_WITH_CONCERNS, NEEDS_CONTEXT, BLOCKED.
- For BLOCKED/NEEDS_CONTEXT, change context/model/scope before retrying.

## Acceptance Criteria

Use observable checks:

- comm

[skill instructions truncated]

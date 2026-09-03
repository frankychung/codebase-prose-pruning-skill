# Codebase Prose Pruning Skill

An [Agent Skills](https://agentskills.io/) workflow for simplifying excessive comments and codebase documentation without changing program behavior or losing constraints.

The skill reviews prose rather than blindly stripping it. It removes narration, duplication, implementation inventories, chronology, and rhetorical buildup while preserving hidden invariants, decisions, evidence, compatibility constraints, safety notes, protocol synchronization, and required attribution.

## Install

### Claude Code

```bash
mkdir -p ~/.claude/skills
git clone https://github.com/frankychung/codebase-prose-pruning-skill.git \
  ~/.claude/skills/codebase-prose-pruning
```

Start or restart Claude Code, then invoke:

```text
/codebase-prose-pruning simplify <path> and its related documentation
```

Claude may also load the skill automatically when you ask it to prune or simplify codebase prose.

### Pi

```bash
git clone https://github.com/frankychung/codebase-prose-pruning-skill.git \
  ~/.agents/skills/codebase-prose-pruning
```

Pi discovers skills under `~/.agents/skills/` when it starts. Restart Pi after installation, then invoke:

```text
/skill:codebase-prose-pruning simplify <path> and its related documentation
```

The skill may also load automatically when you ask Pi to prune or simplify comments, agent instructions, context documents, concept guides, ADRs, or other codebase prose.

### Other Agent Skills-compatible tools

Clone this repository into the tool's skills directory under the name `codebase-prose-pruning`. Consult that tool's documentation for its discovery paths and invocation syntax.

## What it does

1. Reads repository instructions and fixes the cleanup boundary.
2. Separates authored files from generated, vendored, licensed, and binary files.
3. Protects existing uncommitted work.
4. Establishes one source of truth across comments and documentation.
5. Applies separate retention rubrics to source comments and documents.
6. Verifies that non-comment code did not change.
7. Runs repository-specific formatting, tests, linting, asset checks, and link checks.
8. Reports coverage, retained constraints, and before/after measurements.

The included inventory script is deliberately read-only and heuristic:

```bash
python3 scripts/inventory.py path/to/source path/to/tests
```

It helps plan coverage but never edits files or decides which comments survive.

## Safety

Skills can instruct an agent to execute commands and modify files. Review `SKILL.md` and bundled scripts before installing or updating them.

This skill explicitly forbids blanket comment stripping because comment syntax may occur inside strings, templates, fixtures, generated output, or runtime documentation.


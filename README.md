# Comment Pruning Skill

An [Agent Skills](https://agentskills.io/) workflow for removing excessive comments and duplicated documentation without changing program behavior.

The skill makes an agent review comments rather than blindly strip them. It preserves hidden invariants, compatibility constraints, safety notes, protocol synchronization, required attribution, and other knowledge the code cannot express.

## Install

### Pi

```bash
git clone https://github.com/frankychung/comment-pruning-skill.git \
  ~/.agents/skills/comment-pruning
```

Pi discovers skills under `~/.agents/skills/` when it starts. Restart Pi after installation, then invoke:

```text
/skill:comment-pruning clean <path> and its related documentation
```

The skill may also load automatically when you ask Pi to remove, reduce, audit, or simplify comments.

### Other Agent Skills-compatible tools

Clone this repository into the tool's skills directory under the name `comment-pruning`. Consult that tool's documentation for its discovery paths and invocation syntax.

## What it does

1. Reads repository instructions and fixes the cleanup boundary.
2. Separates authored files from generated, vendored, licensed, and binary files.
3. Protects existing uncommitted work.
4. Establishes one source of truth across code comments and documentation.
5. Applies a retention rubric to every authored file in scope.
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


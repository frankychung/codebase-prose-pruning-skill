---
name: codebase-prose-pruning
description: Prune and simplify excessive codebase prose without changing behavior or losing constraints. Use for comments, doc comments, agent instructions, context documents, concept guides, ADRs, duplicated rationale, or verbose codebase documentation.
---

# Codebase Prose Pruning

Make code and documentation easier to read. Remove prose that ordinary local reading can recover while preserving knowledge the code cannot express.

## Process

### 1. Fix the boundary

Read repository instructions first. Resolve these before editing:

- target paths and languages;
- which source comments, tests, examples, assets, and documentation are included;
- authored versus generated, vendored, licensed, and binary files;
- the repository's formatting, test, lint, and documentation gates.

If the request leaves a consequential choice open, ask once with a recommendation. Otherwise proceed.

Run `git status --short` and preserve every pre-existing change. Snapshot the target outside the repository when the worktree is already dirty.

**Complete when:** every target file is classified as authored, generated, vendored, licensed, binary, or out of scope.

### 2. Find the source of truth

Read the architecture and domain documents governing the target. Assign each surviving fact one home:

- agent instructions: actions and landmines;
- context/glossary: architecture and canonical vocabulary;
- concepts: reusable operational constraints;
- ADRs: decisions, alternatives, evidence, and consequences;
- source comments: immediate contracts and invariants.

Treat repository structure and code as sources of truth. Documentation that merely caches an easy lookup is a deletion candidate.

**Complete when:** every document that may receive or duplicate removed rationale has been inspected.

### 3. Inventory, do not strip

Run:

```bash
python3 <skill-dir>/scripts/inventory.py <target>...
```

Use the result to plan coverage, not to decide what survives. Keep a temporary reviewed-file checklist for large scopes.

Never remove comments with a blanket regex or line filter. Comment syntax may occur inside Rust raw strings, JavaScript template literals, fixtures, generated output, or other runtime data.

### 4. Prune comments and simplify documentation

Keep a source comment only when it conveys at least one of:

- a hidden invariant or externally enforced contract;
- a surprising reason the obvious implementation is wrong;
- units, bounds, precision, ordering, timing, or failure semantics not encoded by types;
- a cross-language or protocol synchronization point;
- a safety, security, compatibility, or platform constraint;
- required licensing, attribution, tooling directives, or generated-file provenance.

Remove:

- narration of the next statement;
- symbol and field inventories;
- parameter, return-value, and test-setup paraphrases;
- module tours recoverable from names and imports;
- chronology, milestone notes, issue archaeology, and rhetorical defenses;
- obvious public API documentation;
- duplicate explanations already authoritative elsewhere;
- commented-out code and stale TODOs.

Rewrite surviving comments to the shortest statement that preserves the constraint. Attach ADR or issue references only to a surviving constraint. Sparse section headings may remain in long flat CSS or JavaScript files when they provide real navigation.

Documentation keeps:

- its unique purpose and canonical vocabulary;
- actionable agent instructions and landmines;
- architecture needed to navigate the code;
- an ADR's decision, genuine alternatives, decisive evidence, and consequences;
- operational constraints that apply across files.

Remove duplicated explanations, implementation inventories, chronology, rhetorical buildup, cheap repository lookups, repeated examples, and detail below the document's information tier. Prefer concise pointers over copied rationale. Preserve meaning while shortening sentences and structure.

Read [language traps](references/language-traps.md) for every language in scope.

**Complete when:** every authored source and documentation file in the checklist has been read, every surviving comment passes the retention test, and every document contains only material appropriate to its role.

### 5. Prove behavior stayed fixed

Use targeted edits. Compare the result with the pre-edit snapshot or fixed point after removing comments through a language-aware tokenizer when available. Inspect every reported token difference manually.

Doc comments are not always inert: they may contain doctests, affect generated API documentation, feed type checkers, or be runtime strings. Tool directives and annotations that resemble comments count as code.

Run the repository's formatter, tests, linter, asset/module tests, documentation-link checks, and `git diff --check`. Do not weaken a gate to make the cleanup pass.

**Complete when:** non-comment changes are either absent or explicitly accounted for, every required gate passes, and existing user changes remain intact.

### 6. Report

Report:

- paths and file classes reviewed;
- changed and intentionally unchanged areas;
- retained comment and documentation categories;
- before/after comment counts as evidence, never as a target;
- documentation reductions;
- each validation command and result;
- any non-comment difference and why it is safe.

Do not commit unless asked.

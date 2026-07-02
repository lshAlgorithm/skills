---
name: maintain-agentic-proj
description: "Use when cleaning or maintaining an agentic project's durable workflow files and experiment artifacts: add, clean, rename, remove, or reconcile STATUS.md and optional PLAN.md files; keep parent/child docs synchronized; preserve current status, how to run current workflows, future plans, and concise tried-but-failed status notes; move retained/obsolete runnable recipes into local doc/ files; maintain optional CONTEXT.md and ADR references; and remove legacy/conflicting documentation noise. Prefer STATUS.md-only when the user wants one combined durable state file. Pair with reproducible-logging for run-log and command-audit details."
---

# Maintain Agentic Project

## Goal

Leave the project easier for the next agent or human to understand.

Maintain only useful durable state:

- One coherent `STATUS.md` per folder where durable state is useful.
- Add `STATUS.md` where it improves cooperation; clean or remove it where it creates clutter.
- `STATUS.md` contains current status, how to run current workflows, future plans, retained obsolete intentions, and artifact/detail pointers.
- Current runnable commands belong in `STATUS.md`; obsolete or retained runnable recipes belong in `doc/` under the same folder and are linked from `STATUS.md`.
- Use `PLAN.md` only when the project explicitly keeps a separate plan hierarchy; otherwise merge plan content into `STATUS.md` and remove stale plan files.
- Optional `CONTEXT.md` contains only project-specific vocabulary.
- Optional ADRs record only durable decisions, not status, plans, logs, or ordinary failed attempts.
- No contradictions between parent and child docs.

Do not erase evidence needed for reproducibility. Preserve authoritative raw traces, final reports, and run logs needed to audit the result.

## Audit First

Before editing:

1. Locate project root and likely spec/status area.
2. Find docs and logs:

```sh
find . \( -name PLAN.md -o -name STATUS.md -o -name CONTEXT.md -o -name CONTEXT-MAP.md -o -name '*.log' \)
find . \( -path '*/adr/*.md' -o -name ADR.md \)
```

3. Read parent docs before child docs.
4. Identify authoritative artifacts that docs should describe.
5. Check for stale references to deleted folders, old methods, obsolete run names, and contradicted decisions.

If the user asks to clean a specific folder, scope the audit to that subtree plus its parent docs.

## STATUS.md / PLAN.md Rules

- `STATUS.md` is the durable state map: current status, how to run current workflows, future plans, authoritative artifact pointers, known gaps, and one-sentence tried/failed/obsolete/superseded intentions.
- `PLAN.md` is optional and should exist only when the project explicitly keeps future plans separate from status.
- Parent docs stay high-level; child docs stay local.
- Prefer links or paths over duplicating the same details across levels.
- When preserving history, retain the obsolete intention and reason in one sentence; remove diary detail.
- When preserving retained/obsolete runnable workflows, move exact old commands into a local `doc/` file and link it from `STATUS.md`.
- When preserving future work, keep high-level phases in parent status files and detailed local phases in child status files unless a separate plan hierarchy is explicitly retained.
- If consolidating into `STATUS.md`, delete stale `PLAN.md` files after migrating useful future-plan content.
- If parent and child docs disagree, prefer newer verified artifacts over older prose.
- If a conflict changes project direction and cannot be resolved from evidence, ask the user.

You may add a new `STATUS.md` when current local state or future local phases need durable explanation. You may add `PLAN.md` only when the user or repo convention explicitly requires separate plan files. You may remove either when it is empty, redundant, stale, or better represented elsewhere.

Follow `references/plan-status-hierarchy.md` when changing `PLAN.md` or `STATUS.md`, especially in repos with hierarchy hooks.

## CONTEXT.md / ADR Rules

- Read existing `CONTEXT.md` or `CONTEXT-MAP.md` when project-specific terminology affects the work.
- Create or update `CONTEXT.md` lazily only when a term is actually resolved.
- Keep `CONTEXT.md` free of implementation details, status, plans, and experiment results.
- Create ADRs rarely, only for durable decisions that are hard to reverse, surprising without context, and chosen from real alternatives.
- Use the repo's ADR convention. If none exists, prefer `spec/adr/` for research/spec-heavy repos and `docs/adr/` for ordinary engineering repos.

See `references/context-and-decisions.md` for formats and examples.

## Log Coordination

During maintenance, check logs only enough to decide whether docs and artifacts agree. Use `reproducible-logging` for detailed log cleanup, command capture standards, run naming, and reproducibility audits.

Keep authoritative raw logs referenced by current docs. Remove or archive logs only when they are empty, stale, duplicated, or explicitly obsolete. Do not rewrite raw logs unless the user explicitly asks.

## Run Instructions

For current maintained workflows, keep a compact "How to Run" section in the local `STATUS.md` with exact commands and operational requirements:

- `uv` / `.venv` commands for Python setup and execution.
- `tmux` session names for long runs.
- GPU variables, model paths, endpoints, and log paths when they affect reproducibility.
- The expected output paths.

For obsolete or retained workflows, create or update `doc/<workflow>.md` in the same folder and move old command recipes there. `STATUS.md` should keep only the one-sentence retained intention and a pointer to the doc file.

## Final Report

After maintenance, report:

- Which docs were updated, added, removed, or retained.
- Which folders/logs/artifacts were removed or retained.
- Which conflicts were resolved or escalated.
- Which verification commands were run.

Do not claim the project is clean until verification confirms the remaining docs and artifacts agree.

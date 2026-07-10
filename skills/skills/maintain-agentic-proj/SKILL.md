---
name: maintain-agentic-proj
description: "Use when cleaning or maintaining an agentic project's durable workflow files and experiment artifacts: add, clean, rename, remove, or reconcile STATUS.md and append-only doc/ plan files; keep parent/child docs synchronized; preserve self-contained current status, exact current run commands, artifact pointers, history including tried/failed/superseded notes, and doc/ plan links; maintain optional CONTEXT.md and ADR references; and remove conflicting documentation noise. Pair with reproducible-logging for run-log and command-audit details."
---

# Maintain Agentic Project

## Goal

Leave the project easier for the next agent or human to understand.

Maintain only useful durable state:

- One coherent `STATUS.md` per folder where durable state is useful.
- Add `STATUS.md` where it improves cooperation; clean or remove it where it creates clutter.
- `STATUS.md` is self-contained pickup context: project purpose, current status, exact current runnable commands, artifact/detail pointers, open gaps, and history.
- Whenever a part of the file is fixed, you can defer this part to a new file in folder `doc/` for conciseness of the status file.
- One deferred part should be a coherent block with a reasonable summarization as its name of the new file, not just fragments.
- Planning detail belongs in append-only `doc/<timestamp-or-topic>-plan.md` files under the same folder. Each planning pass creates a new plan file instead of editing old plan files.
- Link to `doc/` plan files and merge failed/obsolete/superseded notes into `History`.
- Optional `CONTEXT.md` contains only project-specific vocabulary.
- Optional ADRs record only durable decisions, not status, plans, logs, or ordinary failed attempts.
- No contradictions between parent and child docs.

Do not erase evidence needed for reproducibility. Preserve authoritative raw traces, final reports, and run logs needed to audit the result.

## Audit First

Before editing:

1. Locate project root and likely spec/status area.
2. Find docs and logs:

```sh
find . \( -name STATUS.md -o -name CONTEXT.md -o -name CONTEXT-MAP.md -o -path '*/doc/*.md' -o -name '*.log' \)
find . \( -path '*/adr/*.md' -o -name ADR.md \)
```

3. Read parent docs before child docs.
4. Identify authoritative artifacts that docs should describe.
5. Check for stale references to deleted folders, old methods, obsolete run names, and contradicted decisions.

If the user asks to clean a specific folder, scope the audit to that subtree plus its parent docs.

## STATUS.md / Planning Rules

- `STATUS.md` is the durable pickup map: purpose, current status, exact current run commands, authoritative artifact pointers, known gaps, relevant `doc/` links, and concise history.
- `STATUS.md` must not depend on chat history for project purpose, current state, or how to run current executable workflows.
- Put plan detail in a new append-only `doc/<timestamp-or-topic>-plan.md` file and link it from `STATUS.md`.
- Parent docs stay high-level; child docs stay local.
- Prefer links or paths over duplicating the same details across levels.
- In hierarchy updates, preserve all current runnable workflows' exact commands at the appropriate local `STATUS.md` level. Include `uv`, `.venv`, `tmux`, GPU vars, model paths, endpoints, output paths, and log paths when relevant.
- Run results, detailed metrics, large tables, raw traces, and long interpretations may be deferred to child folders, reports, summaries, or result artifacts.
- When preserving old runnable workflows, move exact old commands into a local `doc/` file and link it from `STATUS.md`.
- When preserving future work, create a new plan doc under local `doc/`; do not rewrite older plan docs.
- If parent and child docs disagree, prefer newer verified artifacts over older prose.
- If a conflict changes project direction and cannot be resolved from evidence, ask the user.

You may add a new `STATUS.md` when current local state or executable workflows need durable explanation. You may add new `doc/` plan files when future work needs durable planning. You may remove stale `STATUS.md` files when they are empty, redundant, stale, or better represented elsewhere.

Follow `references/plan-status-hierarchy.md` when changing `STATUS.md`, especially in repos with hierarchy hooks.

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

For current maintained workflows, keep a compact `##Reproduce Command` section in the local `STATUS.md` with exact commands and operational requirements:

- `uv` / `.venv` commands for Python setup and execution.
- `tmux` session names for long runs.
- GPU variables, model paths, endpoints, and log paths when they affect reproducibility.
- The expected output paths.

For old or retained workflows, create or update a local `doc/<workflow>.md` and move old command recipes there. `STATUS.md` should keep only the short historical reason and a pointer to the doc file.

For new planning, create a new local `doc/<timestamp-or-topic>-plan.md` file. Do not modify earlier plan files except to fix broken links or obvious factual errors.

## Final Report

After maintenance, report:

- Which docs were updated, added, removed, or retained.
- Which folders/logs/artifacts were removed or retained.
- Which conflicts were resolved or escalated.
- Which verification commands were run.

Do not claim the project is clean until verification confirms the remaining docs and artifacts agree.

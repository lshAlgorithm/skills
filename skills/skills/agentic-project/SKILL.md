---
name: agentic-project
description: Use for long-running or multi-session engineering/research projects, especially academic experiments, agent workflows, benchmark runs, and repo-spanning tasks where Codex should maintain durable STATUS.md project state, artifact organization, optional glossary/decision docs, and honest progress synchronization. Prefer STATUS.md as the combined current/future/obsolete state file unless the repo explicitly keeps PLAN.md. Pair with reproducible-logging when exact run logs, commands, traces, metrics, or audit trails matter.
---

# Agentic Project

## Core Discipline

Treat the project as durable collaboration, not one chat turn.

Maintain enough state that a future agent can recover the work from files:

- Keep a stable project overview near the root. Prefer `spec/` when it fits the repo.
- Prefer `STATUS.md` when a folder needs durable state: current verified status, how to run current workflows, future plans, artifact pointers, open gaps, or concise history of tried/obsolete intentions.
- Use `PLAN.md` only when the project explicitly keeps a separate plan hierarchy; otherwise merge future plans into `STATUS.md`.
- Keep artifacts organized and named so important variables are obvious.
- Keep `README.md` stable and high-level; put current state and temporary details in `STATUS.md`, not `PLAN.md`.

Do not create durable docs mechanically in every folder. Create or update them when they improve continuity, reproducibility, or handoff quality.

## Starting Work

1. Locate the project root and relevant subfolder.
2. Read root/spec docs first, then local `STATUS.md`, optional `PLAN.md`, reports, and result folders.
3. If `CONTEXT.md` or `CONTEXT-MAP.md` exists, use its vocabulary. If it does not exist, proceed silently unless project-specific terms must be resolved.
4. Check decision records only when the task touches durable choices. Follow the repo's convention; in research repos with `spec/`, prefer `spec/adr/` if new ADRs are needed.
5. Explore before asking. Ask only for unresolved product, research, or tradeoff decisions.

Use `reproducible-logging` for exact command capture, tmux run logs, traces, metrics, and run-level audit trails.

## Durable File Roles

- `README.md`: stable entrypoint, project purpose, and pointers to durable docs.
- `STATUS.md`: preferred durable state file containing current status, how to run current workflows, future plans, retained obsolete intentions, and artifact/detail pointers.
- `PLAN.md`: optional future-only plan file for repos that explicitly keep separate plans. If it exists, it should point to the relevant `STATUS.md` for current state and history.
- `CONTEXT.md`: optional glossary of project-specific terms only. Not a plan, status file, or implementation diary.
- ADRs: optional, rare records for durable decisions that are hard to reverse, surprising without context, and based on real tradeoffs.

Reference existing docs by path instead of duplicating the same facts in multiple places.

For runnable workflows:

- Put exact commands for current maintained workflows in the local `STATUS.md`, including required tools such as `uv`, `.venv`, `tmux`, GPU variables, model paths, and log paths when they affect reproducibility.
- Put obsolete or retained runnable workflows under `doc/` in the same folder, then link to those docs from `STATUS.md`.
- Keep `STATUS.md` concise: include current commands directly, but defer old command recipes and detailed logs to `doc/` or result artifacts.

## During Work

- Keep project files aligned with the artifact tree.
- Preserve history decently: do not keep long diaries, but retain obsolete intentions in `STATUS.md` as one sentence each when they explain current choices or prevent rediscovery.
- Preserve future direction decently: keep future plans in `STATUS.md` unless the repo explicitly uses separate `PLAN.md` files.
- Preserve raw traces and raw summaries for academic experiments.
- Record negative results as carefully as positive results.
- Distinguish real-system evidence from simulator/replay evidence.
- Distinguish autonomous agent behavior from scripted fallback or synthetic stress.
- Record setup failures as failures; do not treat blocked traces as valid experimental traces.
- Add focused tests for fragile experiment-support code such as materialization, parsing, artifact organization, and replay conversion.

See `references/academic-evidence.md` when an academic experiment, benchmark, or paper-facing interpretation is involved.

## Completion Standard

Before saying a project stage is done:

1. Re-read the user's actual objective.
2. Verify deliverables against current files and command output.
3. Run relevant tests or validators.
4. Inspect result artifacts, not just exit codes.
5. Update relevant `STATUS.md` files with the final honest interpretation, including one-sentence failed/obsolete/superseded intentions when they explain the result.
6. Check for stale processes if long experiments were run.

If the evidence is weak, say so and keep the next step concrete.

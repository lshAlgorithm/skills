---
name: agentic-project
description: Use for long-running or multi-session engineering/research projects, especially academic experiments, agent workflows, benchmark runs, and repo-spanning tasks where Codex should maintain self-contained STATUS.md project state, artifact organization, append-only doc/ plan files, optional glossary/decision docs, and honest progress synchronization. Pair with reproducible-logging when exact run logs, commands, traces, metrics, or audit trails matter.
---

# Agentic Project

## Core Discipline

Treat the project as durable collaboration, not one chat turn.

Maintain enough state that a future agent can recover the work from files:

- Keep a stable project overview near the root. Prefer `spec/` when it fits the repo.
- Prefer `STATUS.md` when a folder needs durable state: project purpose, current verified status, exact commands for current runnable workflows, artifact pointers, open gaps, and concise history including failed, superseded, or obsolete attempts.
- Point planning readers to current-directory `doc/` plan files instead. Store plans as append-only files under the current directory's `doc/` folder. Each new planning pass creates a new plan file instead of rewriting old plan files.
- Keep artifacts organized and named so important variables are obvious.
- Keep `README.md` stable and high-level; put current pickup state in `STATUS.md`, and put plan details in `doc/`.

Do not create durable docs mechanically in every folder. Create or update them when they improve continuity, reproducibility, or handoff quality.

## Starting Work

1. Locate the project root and relevant subfolder.
2. Read root/spec docs first, then local `STATUS.md`, relevant `doc/` plan files, reports, and result folders.
3. If `CONTEXT.md` or `CONTEXT-MAP.md` exists, use its vocabulary. If it does not exist, proceed silently unless project-specific terms must be resolved.
4. Check decision records only when the task touches durable choices. Follow the repo's convention; in research repos with `spec/`, prefer `spec/adr/` if new ADRs are needed.
5. Explore before asking. Ask only for unresolved product, research, or tradeoff decisions.

Use `reproducible-logging` for exact command capture, tmux run logs, traces, metrics, and run-level audit trails.

## Durable File Roles

- `README.md`: stable entrypoint, project purpose, and pointers to durable docs.
- `STATUS.md`: preferred durable state file. It must be self-contained enough for a future agent or human to quickly pick up the project. It should and only include the titles `#Purpose, `#Current Status` (`##Reproduce commands` is necessary for code folder only), `#History`, `#Artifact/result pointers`, `#Notes and open gaps`. Leave the title without content if nothing to write.
- `doc/<timestamp-or-topic>-plan.md`: append-only planning files. Put detailed plans here, one new file per planning pass. `STATUS.md` should link to the current relevant plan docs.
- `CONTEXT.md`: optional glossary of project-specific terms only. Not a plan, status file, or implementation diary.
- ADRs: optional, rare records for durable decisions that are hard to reverse, surprising without context, and based on real tradeoffs.

Reference existing docs by path instead of duplicating the same facts in multiple places.

For runnable workflows:

- Put exact commands for every current maintained executable workflow in the local `STATUS.md`, including required tools such as `uv`, `.venv`, `tmux`, GPU variables, model paths, endpoints, output paths, and log paths when they affect reproducibility.
- Do not omit runnable code from `STATUS.md` for current workflows. Purpose can be prose-short; current commands must be concrete.
- Put old runnable recipes and detailed plan text under `doc/` in the same folder, then link to those docs from `STATUS.md`.
- Keep `STATUS.md` concise by deferring run results, large tables, raw logs, and detailed interpretation to result artifacts or child folders.

## During Work

- Keep project files aligned with the artifact tree.
- Preserve history decently: do not keep long diaries, but merge failed, obsolete, and superseded intentions into the normal `History` section as one sentence each when they explain current choices or prevent rediscovery.
- Preserve future direction decently: create a new `doc/<timestamp-or-topic>-plan.md` for each new planning pass, then link it from `STATUS.md`.
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
5. Update relevant `STATUS.md` files with purpose, current status, exact current run commands, artifact pointers, and final honest interpretation; merge failed/obsolete/superseded notes into `History`.
6. Check for stale processes if long experiments were run.

If the evidence is weak, say so and keep the next step concrete.

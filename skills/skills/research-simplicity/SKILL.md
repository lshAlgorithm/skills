---
name: research-simplicity
description: Use this skill whenever doing research planning, experimental-method design, metric design, predictor/model design, benchmark interpretation, or proposing hyperparameters without clear evidence. It keeps early research proposals simple, evidence-backed, and generalizable instead of adding arbitrary thresholds, windows, or knobs.
---

# Research Simplicity

Use this skill when proposing research methods, metrics, predictor designs, experimental protocols, or hyperparameters before there is strong evidence or user feedback.

## Core Rule

Start with the simplest generalizable formulation that answers the research question. Add complexity only when there is concrete evidence, a known operational requirement, or an explicit user request.

## Before Proposing a Parameter

Ask these checks internally:

- Is this parameter tied to an operational variable already in the problem, such as a scheduler lead target `x`?
- Is there evidence from current data that this value or threshold is needed?
- Would this value generalize beyond the current trace or benchmark?
- Can the same goal be expressed with fewer knobs?

If the answer is no, do not introduce the parameter yet. State the simpler baseline and what evidence would justify adding complexity later.

## Metric Design

Prefer continuous, interpretable metrics over bucketed hit/miss labels when the user asks to measure prediction gap or estimation error.

Do not invent arbitrary windows such as “3 seconds” unless they come from the system objective, an existing configuration, or measured evidence. If the task already has an operational target, use that target directly.

Example: for scheduling `x` seconds before tool completion, measure finish-time error at the prediction row closest to actual remaining time `x`, rather than creating a new near-finish window.

## Model and Predictor Design

Prefer a simple baseline first:

- one new method at a time,
- one necessary hyperparameter at a time,
- preserve existing baselines for comparison,
- defer rate-regression, stability penalties, hand-tuned thresholds, and special cases until baseline results show they are needed.

When discussing possible future complexity, label it as future work and do not include it in the initial implementation plan.

## Communication Style

Be direct when a proposal lacks evidence. Replace unsupported detail with an operationally grounded simpler alternative.

Bad pattern:

- “Use a 3 second near-finish window” without evidence.

Better pattern:

- “Use the scheduler lead target `x` because it is the actual operational point where prediction accuracy matters.”

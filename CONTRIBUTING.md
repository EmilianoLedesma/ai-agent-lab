# Contributing Guide

## Purpose

This repository is an AI/LLM engineering lab in the planning-to-experimentation lifecycle. Contributions should improve clarity, reproducibility, and measured learning outcomes.

## Workflow expectations

1. Start with a clear question or hypothesis.
2. Scope changes to one concern at a time.
3. Record assumptions and constraints.
4. Capture experiment configuration exactly.
5. Report measurable outcomes and limitations.
6. Link conclusions to evidence, not intuition.

## Reproducibility requirements

- Document hardware/software context for each experiment.
- Version configurations and prompts used for comparisons.
- Distinguish observed data from interpretation.
- Keep raw benchmark artifacts in `benchmarks/` where practical.
- Update `DECISIONS.md` for material architecture changes.

## Change boundaries

- Do not introduce production infrastructure by default.
- Do not expose local services publicly.
- Avoid permanent stack commitments without documented experiments.
- Keep implementations simple, replaceable, and testable.

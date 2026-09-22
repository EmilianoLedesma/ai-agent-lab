# Agent Working Guidelines

These instructions apply to future AI coding agents operating in this repository.

## Core principles

1. Inspect before modifying
2. Experiment before optimizing
3. Measure before concluding
4. Preserve reproducibility
5. Prefer simple, replaceable components
6. Keep architecture modular and reversible
7. Favor local-first designs where practical
8. Preserve gaming/work usability on the primary laptop
9. Security by default
10. Document meaningful experiments and decisions

## Operating expectations

- Do not conflate concepts: **model != agent**.
- Treat model quality claims as task-specific unless supported by evidence.
- Start with read-only tool capabilities when prototyping agent tools.
- Never expose local model servers directly to the public Internet.
- Record assumptions, constraints, and limitations in docs.
- Avoid premature technology lock-in.

## Change workflow

- Read relevant docs and decision history before code or infra changes.
- Make minimal, testable, reversible changes.
- Capture benchmark and experiment context with each meaningful change.
- Update `DECISIONS.md` when architectural direction changes.

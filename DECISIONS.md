# Architecture Decision Log

This file tracks durable, high-impact architectural decisions.

## ADR-0001: Use existing laptop as first laboratory
- Status: Accepted
- Decision: Use current consumer laptop hardware as the initial experimentation platform.
- Rationale: Maximizes learning under realistic constraints.

## ADR-0002: Preserve gaming capability
- Status: Accepted
- Decision: Maintain system usability for normal work and gaming while running experiments.
- Rationale: Enforces practical resource discipline and prevents over-allocation.

## ADR-0003: Local-first architecture
- Status: Accepted
- Decision: Prefer local execution and private networking as the default.
- Rationale: Improves privacy, cost control, and iteration speed.

## ADR-0004: Separate model from agent
- Status: Accepted
- Decision: Keep model inference concerns distinct from agent orchestration concerns.
- Rationale: Enables independent evolution and clearer evaluation.

## ADR-0005: Start with read-only tools
- Status: Accepted
- Decision: Begin agent tool integration with read-only operations.
- Rationale: Reduces risk while establishing tool contracts and controls.

## ADR-0006: Measure before scaling hardware
- Status: Accepted
- Decision: Make upgrade/scaling decisions only after evidence from benchmarks and experiments.
- Rationale: Prevents premature optimization and unnecessary spend.

## ADR-0007: Avoid premature infrastructure
- Status: Accepted
- Decision: Do not commit early to heavy infra components before validated need.
- Rationale: Keeps architecture adaptable during learning phase.

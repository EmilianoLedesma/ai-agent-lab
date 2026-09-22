# AI Agent Lab

A personal AI/LLM engineering laboratory focused on learning-by-building in a disciplined, reproducible way.

## What this project is

This repository is the foundation for a long-term experimentation lab to understand how local and hybrid AI systems behave in real-world engineering workflows.

## Why this exists

The goal is to develop practical, evidence-based understanding of modern LLM systems and agent architectures, then apply those insights to build a local "second brain" that complements Claude Code.

## Learning philosophy

This project prioritizes:

1. Understanding before automation
2. Experimentation before standardization
3. Measurement before conclusions
4. Reproducibility before optimization
5. Incremental complexity over premature architecture

## Initial hardware baseline

- CPU: Intel Core i7-12650H
- GPU: NVIDIA RTX 4060 Laptop GPU (8 GB VRAM)
- RAM: 32 GB
- Storage: 2 TB
- OS: Windows 11

Constraint: the laptop must remain usable for normal development and gaming.

## High-level architecture (conceptual)

Planned layers (to be evaluated and evolved):

- Hardware and operating environment
- Model runtime and model selection
- API/gateway surface
- Context engine and retrieval
- Tool interface layer
- Agent orchestration and memory
- MCP integration
- Networking and access control
- Observability and evaluation

## Repository structure

- `AGENTS.md`: operating principles for coding agents in this repository
- `ROADMAP.md`: staged learning roadmap
- `ARCHITECTURE.md`: conceptual system boundaries and responsibilities
- `EXPERIMENTS.md`: experiment methodology and queue
- `DECISIONS.md`: architecture decision log
- `CONTRIBUTING.md`: reproducible workflow for contributors
- `docs/concepts/`: learning notes for core AI/LLM topics
- `docs/infrastructure/`: infrastructure, networking, and security notes
- `experiments/`: per-experiment records
- `benchmarks/`: benchmarking artifacts and summaries
- `src/`: future implementation code (intentionally empty now)
- `infra/`: future infrastructure code (intentionally empty now)

## Current status

**Planning and architecture phase only.**

No model runtimes, inference servers, agents, MCP servers, RAG pipelines, databases, Docker services, or cloud infrastructure are implemented yet.

## Major learning areas

- Local LLM inference and quantization trade-offs
- Context engineering and retrieval quality
- Tool calling and agent orchestration patterns
- Memory design and MCP integration
- Performance, reliability, and observability
- Evaluation methodology and safety/security defaults

## Non-goals (for this phase)

- Shipping a production assistant
- Locking into a permanent model or infrastructure stack
- Premature optimization or scaling decisions

## Future direction

Candidate technologies to evaluate over time (not selected yet):

- Inference: llama.cpp, Hugging Face Transformers
- APIs: FastAPI
- Storage: PostgreSQL, vector databases
- Networking: Tailscale
- Observability: Prometheus, Grafana, OpenTelemetry

All selections will be made through documented experiments and decision records.

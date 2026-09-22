# Architecture (Conceptual)

This document defines conceptual boundaries for the future system. It intentionally avoids implementation commitments.

## Principle

`Model != Agent`

- **Model**: generates token predictions from input context.
- **Agent**: orchestrates workflows around the model (planning, tool usage, control flow, error handling, memory interactions).

## Concern separation

### 1. Hardware
Physical compute limits (CPU/GPU/RAM/storage), thermals, power, and usability constraints.

### 2. Operating environment
OS configuration, local development ergonomics, process lifecycle, and system stability.

### 3. Model runtime
Execution engine for model inference (candidate examples: llama.cpp, Transformers backends).

### 4. Model
The specific LLM weights and quantization variant selected per experiment/task.

### 5. API gateway
A stable interface boundary that receives requests and applies policy/routing.

### 6. Context engine
Builds model-ready context from instructions, history, retrieved sources, and tool outputs.

### 7. Agent
Decision-making and orchestration layer that structures multi-step execution.

### 8. Tools
External capabilities exposed through explicit contracts, permissions, and safety rules.

### 9. Memory
Persistent state and retrieval strategies for long-term utility and continuity.

### 10. MCP
Protocol-level integration pattern for connecting external capabilities and services.

### 11. Networking
Local-only by default; remote access only through controlled, authenticated, non-public paths.

### 12. Observability
Metrics, traces, and logs needed to understand behavior and evaluate outcomes.

## Candidate stack (evaluation only)

No permanent selections yet. Candidates to evaluate may include:
- Inference/runtime: llama.cpp, Hugging Face Transformers
- API: FastAPI
- Data stores: PostgreSQL, vector databases
- Networking: Tailscale
- Observability: Prometheus, Grafana, OpenTelemetry

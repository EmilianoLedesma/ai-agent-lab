# Experiment Methodology and Queue

## Experiment methodology (standard structure)

Use the template below for all experiments:

- ID
- Date
- Question
- Hypothesis
- Hardware
- Software
- Model
- Configuration
- Variables
- Procedure
- Measurements
- Results
- Interpretation
- Limitations
- Conclusion
- Next experiment

## Measurement guidance

Collect repeatable metrics where possible:
- latency (first token, total response)
- throughput (tokens/sec)
- resource usage (VRAM, RAM, CPU, GPU utilization)
- quality indicators tied to explicit tasks
- failure rate / error modes

## Initial experiment queue

1. Baseline local inference
2. Quantization comparison
3. GPU offloading behavior
4. Context length impact
5. Model size trade-offs
6. Repository retrieval effectiveness
7. Tool calling reliability
8. Agent loop behavior
9. Memory usefulness and staleness
10. Claude + local model collaboration patterns
11. MCP integration viability
12. Secure remote access patterns

All queue items are planning-stage only until implemented as individual experiment records.

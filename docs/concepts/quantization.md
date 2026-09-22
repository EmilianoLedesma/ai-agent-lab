# Quantization (Concept Note)

Quantization reduces model precision (for example, from FP16 to lower-bit formats) to improve speed and memory usage.

Learning goals:
- understand quality/performance trade-offs across quant levels
- measure impact on latency, throughput, and VRAM/RAM
- identify when lower precision is acceptable for specific tasks

Quantization choices will be made through task-specific experiments, not assumptions.

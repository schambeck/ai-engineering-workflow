# Performance Engineer

## Purpose

Evaluate and improve latency, throughput, resource use, and scalability using measurable evidence.

## Inputs

- Target workload and service-level objectives
- Relevant implementation and architecture
- Existing metrics, profiles, traces, or benchmark results

## Responsibilities

1. Define the workload, baseline, and success threshold.
2. Identify the constrained resource before optimizing.
3. Measure representative steady-state and peak behavior.
4. Inspect database access, network calls, allocation, locking, and caching.
5. Validate improvements against correctness and operational tradeoffs.

## Deliverables

- Reproducible benchmark or load-test procedure
- Baseline and post-change measurements
- Bottleneck analysis
- Recommended changes ordered by expected impact
- Capacity and residual-risk notes

## Constraints

- Do not optimize based only on intuition.
- Change one major variable at a time when benchmarking.
- Include warm-up, dataset size, concurrency, and environment details.
- Reject improvements that compromise correctness without explicit approval.

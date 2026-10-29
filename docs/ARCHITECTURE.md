# APEX-OMEGA Architecture

## Purpose

This document records the intended processing pipeline and correctness boundaries for a multi-venue arbitrage system. It is an architecture description, not a claim that every stage is currently implemented or deployed.

## Pipeline

1. **Discovery** — enumerate candidate pools, venues, and executable destinations from supported registries and live sources.
2. **State acquisition** — retrieve chain-specific state at a known block context; track block number/hash and source freshness.
3. **Normalization** — normalize token identities, decimals, fee units, pool state, and quote units without floating-point ambiguity in the execution path.
4. **Invariant-specific quoting** — dispatch to the correct mathematical adapter (for example, CPMM versus concentrated liquidity). Do not treat unlike invariants as interchangeable.
5. **Candidate ranking** — compare executable buy and sell paths using normalized prices and consistent state context.
6. **Complete cost model** — subtract flash-liquidity fees, gas, priority fee/tip, slippage, and other execution costs. A gross spread is not net profit.
7. **Simulation** — test the candidate against a fork or equivalent state-consistent simulation before granting execution permission.
8. **Transaction construction** — encode verified routes and enforce contract, chain, token, amount, and deadline constraints.
9. **Execution gate** — only the explicitly authorized live mode may broadcast. Development and simulation modes must not leak into broadcast paths.
10. **Settlement verification** — verify the transaction receipt and resulting state, then reconcile actual token flows and realized costs.

## Correctness doctrine

> Hard logic protects correctness. Dynamic config controls behavior. Live state controls opportunity. Simulation controls permission. Settlement controls truth.

Configuration may adjust thresholds and policy, but must not override invariant math, chain identity, token accounting, execution authorization, or settlement truth.

## Opportunity and execution-cycle semantics

The intended model assigns each opportunity an identifier and separates two execution cycles:

- **C1** consists of LEG1 (buy) and LEG2 (sell); it is the initial state-mutating cycle.
- **C2** is considered only after C1's receipt is confirmed and post-C1 block/state hashes are recomputed.
- C2 actions are MIRROR, REVERSE, or DO_NOTHING.
- The intended C2 eligibility window is C1 block +1 through +5.
- C2 must not block the primary scanner or liquidation path.

These are design requirements. This repository does not implement the cycle coordinator, receipt-driven state transition, or live transaction executor.

## Candidate eligibility principles

A production candidate should be rejected unless, at minimum:

- its chain and state context are explicit;
- buy and sell destinations are distinct and independently executable;
- both quotes are comparable under correct token decimals and invariant math;
- pool state is fresh relative to measured cycle duration;
- the route is not the same pool on both sides;
- net expected profit remains positive after all relevant costs;
- simulation and execution authorization pass.

Thresholds belong in dynamic configuration; correctness rules do not.

## Adapter boundaries

Each invariant family needs its own reviewed implementation and tests. Examples include constant-product pools, V3-style concentrated liquidity, Algebra-style pools, Balancer weighted/stable/composable pools, Curve StableSwap/crypto pools, PMM pools, and RFQ or aggregator adapters. Protocol names alone are not a substitute for invariant identification.

## Evidence needed for a production claim

- reproducible tests against independent reference vectors;
- block-pinned state acquisition and reorg handling;
- adapter coverage and decimal/fee validation;
- state-consistent fork simulations;
- transaction calldata and authorization review;
- receipt, balance-delta, and realized-cost reconciliation;
- failure, timeout, stale-state, and liquidation-path tests;
- a benchmark harness with environment and methodology documented.

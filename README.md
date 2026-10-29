# APEX-OMEGA Public Engineering Showcase

This repository is the public evidence package for APEX-OMEGA arbitrage research and engineering. It is designed to let grant reviewers and technical evaluators assess the research problem, inspect a concrete reference implementation, reproduce its tests, and distinguish demonstrated work from planned integration—without access to private repositories.

## Research purpose and public evidence

APEX-OMEGA investigates how decentralized-exchange arbitrage opportunities can be discovered, compared, and evaluated using deterministic calculations, current market state, complete transaction costs, simulation, and settlement verification. The central engineering challenge is not simply identifying a price difference: a candidate must remain executable after token-unit normalization, pool-specific pricing rules, fees, gas and other costs, state changes, and transaction-level validation.

This public repository demonstrates a deliberately bounded starting point: an integer-based constant-product automated market maker (CPMM) quote function, tests, architecture notes, and implementation-status disclosures. These artifacts make a portion of the research inspectable and testable. They do not, on their own, demonstrate a profitable or production-deployed trading system.

## Proof of work: repository and commit-count status

The GitHub account currently contains **15 repositories**. The private project portfolio includes **12 private project repositories, with at least 2,372 commits identified across their histories**. This is a verified lower-bound status, **not an exact aggregate commit total**; the full count across all 15 repositories has not yet been independently verified. The figure describes repository history and does not claim that every commit was authored solely by one person. Private implementation details remain private.

## What reviewers can evaluate here

- **Architecture and research framing:** the intended pipeline, trust boundaries, and correctness invariants.
- **Reference implementation:** integer CPMM output quoting using raw token units.
- **Tests and reproducibility:** unit tests for arithmetic, fee behavior, and invalid inputs, with quick-start instructions.
- **Implementation transparency:** explicit distinction between demonstrated components and outstanding integration or validation work.
- **Security boundaries:** guidance on secrets, deployment credentials, and responsible disclosure.

## Status and scope

This repository is a reference implementation and architecture record. It is **not evidence by itself** that a production arbitrage engine is deployed, profitable, fully integrated, or authorized to broadcast transactions. The CPMM helper covers one invariant family only. Concentrated liquidity, Algebra, Balancer, Curve, DODO, RFQ/aggregator adapters, flash-liquidity integration, live RPC ingestion, fork simulation, transaction execution, and settlement verification require their own implementations and evidence.

## Quick start

Requires Python 3.10 or newer.

```bash
python -m venv .venv
# macOS/Linux:
source .venv/bin/activate
# Windows PowerShell:
# .venv\\Scripts\\Activate.ps1
python -m pip install -e ".[dev]"
pytest
```

## Reference quote

```python
from apex_omega_public import quote_cpmm_out

amount_out = quote_cpmm_out(
    amount_in=1_000,
    reserve_in=1_000_000,
    reserve_out=2_000_000,
    fee_bps=30,
)
print(amount_out)  # 1992
```

Inputs are raw integer token units, not human-formatted decimal amounts. Token decimal normalization must occur before using this helper.

## Engineering invariants

- Hard logic protects correctness.
- Dynamic configuration controls behavior.
- Live state controls opportunity.
- Simulation controls permission.
- Settlement controls truth.

The intended pipeline is discovery → state normalization → invariant-specific quoting → candidate ranking → complete cost model → fork simulation → transaction construction → execution gate → receipt and post-state verification. Each stage needs separate implementation and evidence before production readiness can be claimed.

## Repository map

- `docs/ARCHITECTURE.md` — system boundaries and intended flow.
- `docs/IMPLEMENTATION_STATUS.md` — evidence and outstanding validation.
- `src/apex_omega_public/cpmm.py` — integer CPMM quote function.
- `tests/test_cpmm.py` — arithmetic and validation tests.
- `SECURITY.md` — secret-handling and disclosure policy.

## License

No license is granted by this repository unless a license file is added. Do not assume permission to reuse code beyond applicable law.

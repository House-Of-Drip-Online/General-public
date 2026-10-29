# APEX-OMEGA Public Engineering Showcase

This repository is a public-facing engineering evidence package for the APEX-OMEGA arbitrage research architecture. It separates a small, testable reference implementation from claims about the broader system.

## Proof of work: repository and commit-count status

The GitHub account currently contains **15 repositories**. The private project portfolio includes **12 private project repositories, with at least 2,372 commits identified across their histories**. This is a verified lower-bound status, **not an exact aggregate commit total**; the full count across all 15 repositories has not yet been independently verified. The figure describes repository history and does not claim that every commit was authored solely by one person. Private implementation details remain private.

## What is included

- **Architecture:** intended end-to-end pipeline and trust boundaries.
- **Implementation status:** what this repository demonstrates and what still requires independent verification.
- **CPMM reference math:** a deterministic, integer-only constant-product AMM output quote.
- **Tests:** unit tests for arithmetic, fee behavior, and invalid inputs.
- **Security policy:** boundaries for secrets, deployment credentials, and responsible disclosure.

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

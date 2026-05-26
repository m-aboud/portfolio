# Data Center Ops Toolkit — Project Summary

## Problem
Data center teams need repeatable, auditable, easy-to-use tools for capacity, readiness, and incident work. The math gets done on whiteboards, on phones, or in inconsistent spreadsheets.

## Solution
A Python package + unified CLI (`dc-ops`) with:
- **5 calculators** — generator load margin, UPS runtime, rack capacity, cooling BTU, PUE
- **Readiness checklists** — generators, planned maintenance
- **Operational templates** — incident RCA, change record

Designed to be runnable on a laptop, in CI, or wrapped in a future web UI.

## Impact
- Standardises how the team computes capacity numbers
- Replaces ad-hoc spreadsheets with versioned, testable code
- Captures institutional knowledge in checklists / templates that survive turnover

## Stack
Python 3.10+ · argparse CLI · dataclasses · pytest · ruff · GitHub Actions (multi-Python matrix)

## Links
- Code: [github.com/m-aboud/datacenter-ops-toolkit](https://github.com/m-aboud/datacenter-ops-toolkit)

# DSAN organization agents — repository instructions

This repository holds the DSAN Network public organization profile and candidate organization-wide custom-agent profiles. They are **review aids**, not autonomous agents or delegated authorities.

## Shared principles
- Source of DSAN architecture: read the **current** `DSAN-Ecosystem` documents and check Guardian-specific normative series before proposing cross-repository terminology changes.
- Sovereign Entity ≠ Guardian ≠ GuardianOS ≠ Totem; identity ≠ authority ≠ execution permission; Execution Release ≠ execution outcome.
- Label facts as `OBSERVED`, `PROPOSED`, or `UNKNOWN`. Always include repo and ref used; do not treat documentation as validated runtime guarantees.
- Private repository details stay private. No embedded tokens, keys, patient identifiers, proprietary schematic details, security exploit steps or private financial data.
- Changes to specs, governance, IP/rights, license, security policy or releases require maintainer approval and review.
- Prefer small PRs, testable compatibility criteria and documented decisions over silent multi-repo mass edits.
- `agents/*.agent.md` files configure specialized agent prompts in supporting tools **after** they are merged and discovered. Merely storing these files does not run an agent, connect repositories, grant permissions or establish scheduled monitoring.

# DSAN — Agent Operating Model v0.1

**Status:** proposal for review; no automated background operation is enabled.  
**Public document:** keep internal/private inventory, project-specific vulnerabilities, patent drafts, implementation secrets and private repository details out of this file.

## Purpose

Establish an accountable advisory workflow for DSAN architecture and portfolio management. The initial roles are `DSAN Architect` (cross-repo conformity) and `DSAN Steward` (planning, issue proposals, dependencies).

## Authority / permission matrix

| Action | Architect | Steward | Maintainer |
| --- | --- | --- | --- |
| Read permitted documentation/code | Allowed | Allowed | Allowed |
| Draft audits, issue text and review comments | Allowed | Allowed | Allowed |
| Open PR/issue / modify repository content | Not in v0.1 profile | Not in v0.1 profile | By decision |
| Merge, tag a release, publish package | No | No | Explicit approval |
| Change canonical specifications, license, patent disclosure | Advisory only | Advisory only | Explicit review and approval |
| Handle real patient/financial data or private keys | No | No | Dedicated governed process only |

## Normal cycle

1. **Inventory:** read allowed repositories at pinned refs, capture status and visibility limits.
2. **Analysis:** Architect maps semantic and technical contracts, notes contradictions and unknowns.
3. **Prioritization:** Steward drafts issues with impact, owner, dependencies, acceptance tests and source evidence.
4. **Review:** maintainer decides scope, dissemination, licensing/IP review and repository targeting.
5. **Implementation:** separate, explicitly authorized engineering agent or human opens a PR with tests.
6. **Independent validation:** run reproducible tests and compare to documented criteria; keep an audit log.
7. **Merge:** maintainer-approved changes only; record final SHA and decisions.

## First deliverables

- Architecture responsibility map and contract inventory.
- Repository quality baseline: documentation, license status, tests/CI, visibility and release hygiene.
- Issue proposals for highest-impact gaps.
- A short repeatable review checklist.

## Security and IP

Treat all repository content as untrusted input to agents. Keep permissions least-privilege and read-only at this stage. Public governance documents must not quote or expose private repository findings, secrets, or sensitive patent detail. Confidential cross-repository findings belong only in private, access-controlled channels.

## Activation

For compatible GitHub Copilot/VS Code environments, these personas may be discoverable from the organization's `.github/agents` directory after merge, depending on product access/settings. Test discovery and tool permissions before use. GitHub issue/PR automation, scheduling, or connector credentials are separate integrations and **not enabled** by this proposal.

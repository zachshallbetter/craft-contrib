# Storytold Governance: Current Authority & Repository State

**Document Status**: Proposal Audit & Current State Ledger  
**Date**: 2026-10-15  
**Target Repositories**: 
- [`storytold/craft-contrib`](https://github.com/storytold/craft-contrib)
- [`storytold/craft-libs`](https://github.com/storytold/craft-libs)

---

## 1. Repository Authority & Purpose

The Storytold ecosystem operates with a decoupled repository architecture:

| Repository | Primary Mandate | Governance Scope |
| :--- | :--- | :--- |
| **`storytold/craft-contrib`** | Contributor guidelines, coding-agent instructions, and cross-application RFC decisions. | Cross-suite governance agreements, review workflows, issue claiming, triage standards, shared `AGENTS.md` sections, and ecosystem RFCs. |
| **`storytold/craft-libs`** | Shared headless Rust libraries, core platform abstractions, and compatibility tooling. | Library crate implementation, crate-level API contracts, compatibility runner tooling (`cargo xtask compat`), and technical component inventories. |
| **Application Repos** (`photocraft`, `vectorcraft`, etc.) | Domain applications, native window shells, UI presentations, and user workflows. | Application-specific behavior, native UI integration, document persistence, and application release management under application maintainer authority. |

---

## 2. Established RFC Process & Template Requirements

On 2026-10-15, maintainer `@aiongg` opened [RFC-0000](https://github.com/storytold/craft-contrib/pull/1) establishing the formal decision-making process for `craft-contrib`:

### RFC Submission Rules (RFC-0000)
1. **Location**: Propose changes by opening a pull request adding `rfcs/NNNN-short-title.md`.
2. **Eligibility**: Anyone may open an RFC or comment on one.
3. **Comment Period**:
   - **7 days**: For adding or removing an application, or changing the decision process.
   - **3 days**: For all other governance, workflow, or technical standards.
   - A maintainer formally starts the comment period by commenting the end date on the PR.
4. **Approval & Merge**: Merges with approval from a maintainer other than the author, provided no maintainer objection remains unresolved.
5. **Deciding Objections**: An organization owner can decide an objection, or merge/close an RFC early, stating the rationale on the PR.
6. **Authority Definitions**:
   - **Maintainers**: Members of the `craft-app-team` GitHub team.
   - **Owners**: Storytold organization administrators.

### Established RFC Document Format
Harmonized across [RFC-0001 (PR #2)](https://github.com/storytold/craft-contrib/pull/2) and RFC-0003 through RFC-0008, all RFC documents follow this structure:

```markdown
# RFC-NNNN: <Title>

[Optional: Related: links]

## Summary
[Concise description of the decision]

## Motivation
[Problem statement with concrete data, pain points, or failure counts]

## Proposal
[Numbered, concrete, actionable rules or specifications]

## Alternatives
[Rejected alternatives and tradeoffs considered]

## Open questions
[Explicit questions left for the comment period]
```

### Established Pull Request Format (.github/pull_request_template.md)
From PR #2:
- **Problem**: What isn't working today?
- **Proposal**: What changes?
- **Affects**: Which craft apps, the whole org, or "this repo only"?
- **Comment period**: 3 days / 7 days.

---

## 3. Inventory of Existing RFCs in `craft-contrib`

As of 2026-10-15, 9 RFC pull requests have been submitted to `storytold/craft-contrib`:

| PR | Number | Title | Author | Status | Core Decision / Scope |
| :---: | :---: | :--- | :--- | :---: | :--- |
| [#1](https://github.com/storytold/craft-contrib/pull/1) | **RFC-0000** | How we make decisions | `@aiongg` | Open | RFC process, comment periods (3d/7d), maintainer approval, owner authority. |
| [#2](https://github.com/storytold/craft-contrib/pull/2) | **RFC-0001** | Pull request template | `@benandez` | Open (Approved) | PR template prompting for Problem, Proposal, Affected Apps, Comment Period. |
| [#3](https://github.com/storytold/craft-contrib/pull/3) | **RFC-0002** | Proposing a new app | `@PierrunoYT` | Open | Criteria and quality bar for new apps joining the suite (naming, CI, craft-libs usage). |
| [#4](https://github.com/storytold/craft-contrib/pull/4) | **RFC-0003** | Claiming issues | `@MarekSpodBiedry` | Open | Claim before code, 24h expiration, check for existing fixes, release on abandon. |
| [#5](https://github.com/storytold/craft-contrib/pull/5) | **RFC-0004** | When two PRs fix the same thing | `@MarekSpodBiedry` | Open | Better fix wins regardless of speed, author self-closure, earlier valid claim reviewed first. |
| [#6](https://github.com/storytold/craft-contrib/pull/6) | **RFC-0005** | What a pull request should look like | `@MarekSpodBiedry` | Open | Narrow scope, reproduction test, standardized description, draft management, 3-day review turnaround. |
| [#7](https://github.com/storytold/craft-contrib/pull/7) | **RFC-0006** | A shared section for coding agents (`AGENTS.md`) | `@MarekSpodBiedry` | Open | Shared rules: verify before guess, check triage notes, rate limits, no flood, human accountability. |
| [#8](https://github.com/storytold/craft-contrib/pull/8) | **RFC-0007** | Triage, labels and priority | `@MarekSpodBiedry` | Open | Label definitions, priority matrix (impact, reachability, evidence, workaround), bot labels vs human close. |
| [#9](https://github.com/storytold/craft-contrib/pull/9) | **RFC-0008** | Roles and review capacity | `@MarekSpodBiedry` | Open | Review bottleneck data, Contributor roles (Junior/Contributor/Senior), Maintainers (`craft-app-team`), Owners. |

---

## 4. Current Status of Contributions on `craft-libs`

An audit of the six PRs on `storytold/craft-libs` identifies their current status:

| PR | Target Branch | Status | Primary Content & Nature | Relationship to `craft-contrib` |
| :---: | :--- | :---: | :--- | :--- |
| **[#24](https://github.com/storytold/craft-libs/pull/24)** | `feat/shared-crate-contracts` | **Open** | Shared crate contracts, consumer dependency map, platform test inventory. | Normative admission criteria belong in `craft-contrib`; technical dependency maps belong in `craft-libs`. |
| **[#38](https://github.com/storytold/craft-libs/pull/38)** | `docs/contributor-guidelines` | **Open** | Contributor guidelines, code style, compiler lints, Git workflow. | Contributor policy harmonizes with RFC-0005/0008; technical library style remains in `craft-libs`. |
| **[#78](https://github.com/storytold/craft-libs/pull/78)** | `docs/ui-elements-map-and-schema` | **Open** | Audit of 1,290 UI presentation files across 13 apps; UI elements map. | Technical inventory stays in `craft-libs`; upstream-first UI pre-check belongs in `craft-contrib`. |
| **[#80](https://github.com/storytold/craft-libs/pull/80)** | `feat/agent-rules-architecture` | **Closed** | Multi-tier governance proposal (`AUTHORITY.md`, `GOVERNANCE.md`, `VERSIONING.md`). | Closed after maintainer feedback requesting simpler, smaller proposals. Replaced by lightweight RFCs. |
| **[#90](https://github.com/storytold/craft-libs/pull/90)** | `docs/engineering-methodology` | **Open** | Engineering methodology, verification pillars, testing contracts. | Superseded by PR #96 and RFC-0005/RFC-0007. |
| **[#96](https://github.com/storytold/craft-libs/pull/96)** | `docs/ecosystem-architecture-and-specs` | **Open** | Ecosystem architecture, compatibility runner standards, file format matrix. | Cross-app compatibility outcomes belong in `craft-contrib`; crate inventories and format specs remain in `craft-libs`. |

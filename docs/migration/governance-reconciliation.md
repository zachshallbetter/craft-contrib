# Storytold Governance Reconciliation: Overlap, Deduplication & Harmonization

**Document Status**: Proposal Reconciliation & Conflict Resolution Ledger  
**Date**: 2026-10-15  
**Context**: Transition of ecosystem governance from `storytold/craft-libs` to `storytold/craft-contrib` following maintainer directives.

---

## 1. Analysis of Overlap with Existing `craft-contrib` RFCs (RFC-0000–RFC-0008)

Between 2026-10-15T08:00Z and 2026-10-15T15:00Z, community contributors and maintainers submitted nine initial RFCs to `storytold/craft-contrib`. A reconciliation against earlier proposals in `craft-libs` PRs #38 and #80 shows where existing RFCs already address these topics:

### Table 1: Overlap and Harmonization Analysis

| Established RFC | Proposed By | Core Subject | Overlapping Content in Zach's PRs | Reconciliation Determination |
| :--- | :--- | :--- | :--- | :--- |
| **RFC-0000** | `@aiongg` | Decision Process | PR #80 (`GOVERNANCE.md` voting/RFC rules) | **Fully Superseded**: Adopt RFC-0000 as authoritative decision framework. Do not re-propose decision rules. |
| **RFC-0001** | `@benandez` | PR Template | PR #38 (Section 6.3 PR description format) | **Harmonized**: PR #38's description structure maps directly to RFC-0001 prompts. |
| **RFC-0002** | `@PierrunoYT` | Proposing a New App | PR #96 (Application admission criteria) | **Complementary**: RFC-0002 governs *application* admission; our proposals govern *shared crate* admission. |
| **RFC-0003** | `@MarekSpodBiedry` | Claiming Issues | PR #38 (Section 8.1 "Claim before you start") | **Fully Addressed**: RFC-0003 formalizes the 24h claiming rule, comment syntax, and check-first workflow. Endorse RFC-0003; do not submit competing claim RFC. |
| **RFC-0004** | `@MarekSpodBiedry` | Overlapping PRs | Issue #134 & PR #24 (Resolution of overlaps) | **Fully Addressed**: Formalizes maintainer rule: better fix wins regardless of speed, author closes losing PR. Endorse RFC-0004. |
| **RFC-0005** | `@MarekSpodBiedry` | PR Standards | PR #38 (Section 6.4 PR standards) | **Harmonized**: RFC-0005 covers narrow scope, reproduction test, and draft state. Complementary to compatibility verification. |
| **RFC-0006** | `@MarekSpodBiedry` | Shared `AGENTS.md` | PR #80 (Modular `.agents/rules/` system) | **Reconciled**: Marek's 9-point lightweight section replaces PR #80's rejected 27-file framework, satisfying maintainer simplicity requirements. |
| **RFC-0007** | `@MarekSpodBiedry` | Triage & Priority | PR #90 & PR #96 (Priority & evidence taxonomy) | **Harmonized**: RFC-0007 weighs impact, reachability, evidence, and workaround. |
| **RFC-0008** | `@MarekSpodBiedry` | Roles & Review Capacity | PR #38 (Section 10 Discord roles via TicketCraft) | **Fully Addressed**: Formalizes Contributor, Junior Contributor, Senior Contributor, Maintainer, Owner. Do not re-propose role definitions. |

---

## 2. Extraction & Separation of Concerns

To prevent bloat and maintain clear repository boundaries, existing work is partitioned strictly into **Normative Governance (RFCs)** and **Technical Reference / Implementation**:

### 1. PR #24 (`feat/shared-crate-contracts`)
- **Extract to `craft-contrib`**:
  - The **Two-Consumer Default Threshold**: A crate is normally admitted to `craft-libs` when required by at least two independent applications, with explicit documented exceptions for foundational capabilities (security, auth, interoperability, platform).
  - The **Zero App Code Invariant**: Shared crates must never depend on any application crate.
- **Retain in `craft-libs`**:
  - `docs/consumer-dependency-map.json` & `docs/platform-test-inventory.json` (technical reference).
  - Implementation contracts for `craft-atomic`, `craft-settings`, and `craft-quit` (`docs/contracts.md`).

### 2. PR #38 (`docs/contributor-guidelines`)
- **Harmonize with `craft-contrib`**:
  - Contributor expectations, review turnaround, and role recognition are settled by RFC-0005 and RFC-0008.
- **Retain in `craft-libs`**:
  - `CONTRIBUTING.md` containing repository-specific Rust toolchain instructions (Edition 2024, MSRV 1.95).
  - Compiler lints (`clippy::unwrap_used`, `clippy::panic`).
  - Library-specific code style (`docs/code-style-and-lints.md`) and defensive programming patterns (`.get()`, char-boundary slicing).

### 3. PR #78 (`docs/ui-elements-map-and-schema`)
- **Extract to `craft-contrib`**:
  - **Existing Component Assessment**: Before implementing presentation widgets in application trees, contributors check `craft-ui` to evaluate reuse, while preserving justified application-specific implementations.
- **Retain in `craft-libs`**:
  - `docs/ui-elements-map.md` (the 1,290-file point-in-time reference audit).

### 4. PR #80 (`feat/agent-rules-architecture`)
- **Extract to `craft-contrib`**:
  - **Technical Status Reporting**: Distinguishing Documented, Implemented, Tested, and Empirically Validated without asserting universal supremacy over application-level technical ownership.
  - **Epistemic Restraint on Primitives**: Shared primitives are not full application contracts; unit-tested dispatch is not physical durability.
- **Discard / Retain Locally**:
  - Discard the 27-file multi-tier directory structure rejected by maintainers.

### 5. PR #96 (`docs/ecosystem-architecture-and-specs`)
- **Extract to `craft-contrib`**:
  - **Compatibility Verification Outcomes**: Affected consumer identification, isolated testing, baseline comparison, non-vacuous assertion proof, and reproducible provenance.
- **Retain in `craft-libs`**:
  - `docs/crate-audit.md` (358-crate inventory across checkouts).
  - `docs/document-compatibility.md` (Open file format matrix: PDF, SVG, TIFF, OpenEXR, IDML, etc.).
  - `docs/media-infrastructure.md` (ISOBMFF, audio DSP formulas, bitstream parsing).
  - `docs/migration-plan.md` (candidate extraction roadmaps).

---

## 3. The 4 Focused Candidate RFCs for `craft-contrib`

By eliminating duplication with RFC-0000 through RFC-0008, the remaining technical governance condenses into four focused, independently decidable proposals:

```
┌────────────────────────────────────────────────────────────────────────┐
│               RECOMMENDED CANDIDATE RFC SERIES                         │
├────────────────────────────────────────────────────────────────────────┤
│ 1. RFC-0009: Shared Infrastructure Admission                           │
│    Decision: When functionality belongs in craft-libs vs. apps        │
│    Key Rules: Two-Consumer default threshold, documented exceptions,   │
│               Zero App Code Invariant, separation of concerns          │
├────────────────────────────────────────────────────────────────────────┤
│ 2. RFC-0010: Shared Infrastructure Adoption and Compatibility          │
│    Decision: Required verification outcomes before adopting crates     │
│    Key Rules: Affected consumer identification, isolated testing,      │
│               baseline comparison, non-vacuous checks, provenance      │
├────────────────────────────────────────────────────────────────────────┤
│ 3. RFC-0011 (Held): Technical Reporting Standards and Epistemic Status │
│    Decision: Standard vocabulary for technical claims in discussions   │
│    Key Rules: Documented ≠ Implemented ≠ Tested ≠ Empirically Validated│
│               Respect for maintainer authority and app-level ownership │
├────────────────────────────────────────────────────────────────────────┤
│ 4. RFC-0012 (Held): Shared UI Presentation Assessment                  │
│    Decision: Evaluating shared UI components before authoring duplicates│
│    Key Rules: Check craft-ui first, preserve application-specific      │
│               requirements, conditional extraction on demonstrated need│
└────────────────────────────────────────────────────────────────────────┘
```

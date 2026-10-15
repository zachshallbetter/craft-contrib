# Storytold Governance Migration Inventory & Traceability Matrix

**Document Status**: Proposal Audit & Traceability Ledger  
**Date**: 2026-10-15  
**Sources Audited**:
- `storytold/craft-libs#24` (`feat/shared-crate-contracts`)
- `storytold/craft-libs#38` (`docs/contributor-guidelines`)
- `storytold/craft-libs#78` (`docs/ui-elements-map-and-schema`)
- `storytold/craft-libs#80` (`feat/agent-rules-architecture`)
- `storytold/craft-libs#90` (`docs/engineering-methodology`)
- `storytold/craft-libs#96` (`docs/ecosystem-architecture-and-specs`)

---

## 1. Proposal Classification & Epistemic Audit

Each proposal is classified into one of seven structural categories and assessed under the **Four-Tier Claim Taxonomy**:

$$\text{Documented} \neq \text{Implemented} \neq \text{Tested} \neq \text{Empirically Validated}$$

### Table 1: Comprehensive Inventory of Extracted Proposals

| ID | Origin | Title & Description | Proposal Classification | Current Maturity | Ecosystem Decision Required? | Proposed Destination |
| :---: | :---: | :--- | :--- | :--- | :---: | :--- |
| **P-01** | PR #24 | **Two-Consumer Default Threshold**: Shared crates normally require $\ge 2$ consumer applications before admission, with documented exceptions for foundational capabilities (security, auth, interoperability, platform). | Shared Infrastructure Contract | Proposed policy; observed in candidate extractions (`craft-atomic`, `craft-settings`, `craft-quit`) | **Yes** (RFC) | `craft-contrib` RFC: Shared Infrastructure Admission |
| **P-02** | PR #24 | **Zero App Code Invariant**: Shared crates in `craft-libs` must never depend on any application crate. | Architecture Constraint | Implemented locally in `craft-libs` configuration; proposed as ecosystem policy | **Yes** (RFC) | `craft-contrib` RFC: Shared Infrastructure Admission |
| **P-03** | PR #24 | **Crate Extraction Protocol**: Phased qualification process (Discovery, API Specification, Extraction, Consumer Integration). | Shared Infrastructure Contract | Documented proposal | **Yes** (RFC) | `craft-contrib` RFC: Shared Infrastructure Admission |
| **P-04** | PR #24 | **Isolated Compatibility Testing**: Testing proposed library changes against consumers without contaminating working trees. | Verification Protocol | Implemented tool (`cargo xtask compat` in PR #9); proposed as verification outcome | **Yes** (RFC) | `craft-contrib` RFC: Shared Infrastructure Adoption |
| **P-05** | PR #24 | **Consumer Dependency Map**: Reference mapping of application dependencies on `craft-libs` crates. | Reference Documentation | Documented point-in-time inventory | No (local reference) | Retain in `craft-libs/docs/` |
| **P-06** | PR #38 | **Library Code Quality Standards**: Compiler lints, panic-freedom, unsafe restrictions, clean-room standards. | Engineering Standard | Implemented as local crate lints and CI checks within `craft-libs` | No (library policy) | Retain in `craft-libs` documentation |
| **P-07** | PR #38 | **Defensive Engineering Patterns**: Defensive slicing, checked arithmetic, bounded allocations, lock recovery. | Engineering Standard | Implemented in `craft-libs` source code | No (library style) | Retain in `craft-libs/docs/code-style-and-lints.md` |
| **P-08** | PR #38 | **Git Hygiene & Issue Timeline Cleanliness**: Single squashed commit per PR; avoid issue references in scratch commits. | Workflow Standard | Proposed practice; observed in issue timeline behavior | No | Harmonize with `craft-contrib` RFC-0005 |
| **P-09** | PR #38 | **Small-Batch Landings**: Merges to `main` should occur in small, bisectable batches rather than monolithic integration dumps. | Workflow Standard | Proposed practice; observed in DesignCraft PR #420 regression | No | Harmonize with `craft-contrib` RFC-0005 |
| **P-10** | PR #38 | **Community Contributor Roles**: Junior Contributor, Contributor, Senior Contributor recognition. | Governance Policy | Implemented via Discord bot automation | **Already Proposed** | Covered by `craft-contrib` RFC-0008 (PR #9) |
| **P-11** | PR #78 | **Existing Component Assessment**: Before authoring presentation widgets in application trees, check `craft-ui` to evaluate potential reuse, while permitting justified local controls. | Presentation Guideline | Proposed policy | **Yes** (RFC) | `craft-contrib` RFC: Shared UI Governance |
| **P-12** | PR #78 | **Suite-Wide UI Elements Map**: Descriptive snapshot of 1,290 presentation files across 13 applications. | Reference Documentation | Repository inventory / static code scan | No (technical asset) | Retain in `craft-libs/docs/ui-elements-map.md` |
| **P-13** | PR #78 | **Shared UI Presentation Boundary**: Reusable layout surfaces and theme infrastructure in `craft-ui`; domain commands, translations, and brand styling in applications. | Architecture Boundary | Proposed boundary; partially implemented in `craft-ui` widgets | **Yes** (RFC) | `craft-contrib` RFC: Shared UI Governance |
| **P-14** | PR #80 | **Accurate Technical Status Reporting**: Standard definitions distinguishing Documented, Implemented, Tested, and Empirically Validated. | Reporting Standard | Proposed standard; applied in review comments | **Yes** (RFC) | `craft-contrib` RFC: Technical Reporting Standards |
| **P-15** | PR #80 | **Epistemic Restraint on Primitives**: Shared primitives are not full application contracts; unit-tested dispatch is not physical durability. | Reporting Standard | Documented principle | **Yes** (RFC) | `craft-contrib` RFC: Technical Reporting Standards |
| **P-16** | PR #80 | **Independent Semantic Versioning**: Independent crate release tracks; avoid inferring compatibility from matching numbers. | Versioning Policy | Documented; applied in v0.1.0 release planning | No (library policy) | Retain in `craft-libs/docs/` |
| **P-17** | PR #80 | **Clean-Room Open Standards Policy**: Technical specifications reference public open formats (ISO, SMPTE, ICC, W3C) rather than proprietary product names. | Governance Policy | Applied in crate naming and documentation | No | Retain in contributor documentation |
| **P-18** | PR #80 | **Retention of Negative Results**: Preserving records of disproven architectures and rejected designs. | Engineering Standard | Documented record (13 negative results logged) | No (library record) | Retain in `craft-libs/docs/negative-results.md` |
| **P-19** | PR #90 | **Pillars of Engineering Methodology**: Testing oracles, contracts, qualification, fallback architectures. | Superseded Material | Superseded | No | Superseded by PR #96 |
| **P-20** | PR #96 | **Ecosystem Architecture Topology**: Decoupled multi-tier model across governance, shared libraries, and applications. | Architecture Model | Proposed model; partially reflected in repository separation | No | Documented in `craft-libs` architecture |
| **P-21** | PR #96 | **Shared Extraction Roadmap**: Phased roadmaps for candidate shared crates. | Reference Documentation | Documented proposals | No (planning roadmap) | Retain in `craft-libs/docs/migration-plan.md` |
| **P-22** | PR #96 | **Document Compatibility Reference**: Open format specifications (PDF, SVG, TIFF, OpenEXR, IDML, etc.). | Reference Documentation | Documented reference | No (domain reference) | Retain in `craft-libs/docs/document-compatibility.md` |
| **P-23** | PR #96 | **Downstream Adoption Verification**: Required verification outcomes before consumer applications update dependency pins. | Verification Protocol | Proposed standard | **Yes** (RFC) | `craft-contrib` RFC: Shared Infrastructure Adoption |
| **P-24** | PR #96 | **Suite Crate Audit**: Reconciled inventory of 358 member crates across 14 repository checkouts. | Reference Documentation | Repository inventory / static workspace scan | No (audit snapshot) | Retain in `craft-libs/docs/crate-audit.md` |

---

## 2. Traceability Matrix: Original Sources to Proposed Destinations

The following matrix maps each original document section in `storytold/craft-libs` to its target destination, cleanly separating ecosystem-level decisions from repository-level implementation:

```
┌────────────────────────────────────────────────────────────────────────────────────────┐
│                        CRAFT-LIBS ORIGINAL CONTRIBUTIONS                               │
│  PR #24: Shared Crate Contracts             PR #38: Contributor Guidelines             │
│  PR #78: UI Elements Map                    PR #80: Authority & Governance             │
│  PR #90: Engineering Methodology            PR #96: Ecosystem Architecture             │
└──────────────────────────────────────────┬─────────────────────────────────────────────┘
                                           │
                    Reconciliation & Separation of Concerns
                                           │
         ┌─────────────────────────────────┴──────────────────────────────────┐
         │                                                                    │
         ▼                                                                    ▼
┌──────────────────────────────────────────────┐     ┌──────────────────────────────────────────────┐
│        CRAFT-CONTRIB (GOVERNANCE RFCs)       │     │     CRAFT-LIBS (TECHNICAL IMPLEMENTATION)    │
├──────────────────────────────────────────────┤     ├──────────────────────────────────────────────┤
│ RFC Candidate 0009:                          │     │ Local Reference Assets:                      │
│ - Shared Infrastructure Admission            │     │ - docs/ui-elements-map.md (UI file scan)     │
│   (Default 2 Consumers with Exceptions,      │     │ - docs/crate-audit.md (Crate inventory)      │
│    Zero App Code Invariant)                  │     │ - docs/document-compatibility.md (Formats)   │
│                                              │     │ - docs/negative-results.md (Design records)  │
│ RFC Candidate 0010:                          │     │                                              │
│ - Shared Infrastructure Adoption             │     │ Technical Tooling & Libraries:               │
│   (Isolated Testing, Baseline Comparison,    │     │ - cargo xtask compat runner implementation   │
│    Non-Vacuous Verification, Provenance)     │     │ - Shared crates (atomic, settings, quit, ui) │
│                                              │     │                                              │
│ RFC Candidate 0011 (Held for Refinement):    │     │ Contributor & Code Style Guides:             │
│ - Technical Reporting & Epistemic Claims     │     │ - CONTRIBUTING.md (PR #38, repo specifics)   │
│   (4-Tier Status Taxonomy, Respect for       │     │ - docs/code-style-and-lints.md               │
│    Maintainer & App Authority)               │     │ - docs/ci-and-verification.md                │
│                                              │     │                                              │
│ RFC Candidate 0012 (Held for Refinement):    │     │                                              │
│ - Shared UI Presentation Governance          │     │                                              │
│   (Existing Component Assessment,            │     │                                              │
│    Preserve Local Application Requirements)  │     │                                              │
└──────────────────────────────────────────────┘     └──────────────────────────────────────────────┘
```

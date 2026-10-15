# RFC-0011: Technical reporting standards and epistemic claims

Related: storytold/craft-libs#80, storytold/craft-libs#96.

## Summary

This RFC establishes standard definitions for reporting technical status in pull requests, documentation, and issue discussions across Storytold repositories. It defines clear distinctions between design intent, implemented behavior, automated verification, and operational validation. This proposal does not change existing maintainer authority or application-specific technical ownership.

## Motivation

In a multi-repository ecosystem with active contributors and coding agents, ambiguous status claims create confusion about what is operational versus what is merely proposed or partially tested. Pull requests and design documents sometimes describe features as "implemented" when they are only specified, or claim "hardware crash durability" when only operating system call ordering was unit-tested.

Additionally, past governance proposals attempted to introduce broad hierarchies of authority that risked overriding application-specific specifications and maintainer technical judgment. Maintainers rejected that approach.

A simpler reporting standard clarifies technical claims without imposing an elaborate governance hierarchy or infringing on repository-specific technical ownership.

## Proposal

1. **Accurate Technical Status Reporting**: Technical claims in pull requests, documentation, and architectural discussions must accurately describe the maturity of the work. Contributors must distinguish design intent, implemented behavior, automated verification, and operational validation:
   - *Design intent (documented)*: The design, contract, or behavior is described in an RFC, specification, docstring, or issue description, but functional code has not yet been written.
   - *Implemented behavior*: Functional code exists in the repository matching the described behavior.
   - *Automated verification (tested)*: The implementation passes automated tests in an isolated test harness or synthetic environment.
   - *Operational validation (empirically validated)*: The implementation has been verified under real operational conditions, such as against native platform APIs, real-world hardware, or downstream consumer binaries under real workloads.
   These are distinct kinds of evidence, not a mandatory sequential maturity ladder. Claims should identify the specific evidence supporting them without implying that one category automatically establishes another.

2. **Epistemic Restraint on Shared Primitives**:
   - A merged primitive crate (such as atomic file writes or lifecycle handlers) provides a reusable building block, not an end-to-end application contract. Full application guarantees (such as dirty document recovery, unsaved changes confirmation, or multi-window persistence) require implementation and testing inside each consuming application.
   - Unit tests that verify system call dispatch ordering (such as flushing and syncing files before renaming) demonstrate software dispatch order, not survival across physical power interruption or unbuffered hardware drive controllers. Technical descriptions must state exact software guarantees without asserting unverified physical durability.

3. **Preservation of Maintainer Authority and Technical Ownership**:
   - Accepted RFCs in `craft-contrib` establish shared organizational agreements, workflow policies, and cross-application standards.
   - Accepted RFCs do not override application-specific technical ownership, repository maintainer authority, or domain-specific implementation decisions within individual application repositories.
   - Application maintainers retain full authority over their repository architecture, technical trade-offs, and dependency adoption.

## Alternatives

- **Universal hierarchy of authority**: Subordinating application specifications and code to centralized RFCs was previously proposed in PR #80 and rejected because it centralizes decisions excessively and conflicts with application maintainer authority.
- **Strict sequential maturity ladder**: Treats evidence types as rigid progression gates, failing to acknowledge that features may be empirically tested before complete automated suites exist, or that specifications can document existing implementations.
- **Informal claim terminology without definitions**: Allows conflating planned designs with running code, increasing review burden and obscuring the actual status of features across the suite.

## Open questions

- How should pull request descriptions and review comments reference these reporting terms without creating unnecessary administrative overhead for small bug fixes?

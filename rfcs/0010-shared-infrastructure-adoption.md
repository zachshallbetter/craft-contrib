# RFC-0010: Shared infrastructure adoption and compatibility

Related: storytold/craft-libs#9, storytold/craft-libs#24, storytold/craft-libs#96.

## Summary

This RFC establishes the verification requirements for proposing shared library changes and adopting them into consuming applications. Contributors must identify affected consumer applications, verify compatibility in isolated environments without contaminating working trees, compare candidate results against committed baselines, ensure non-vacuous test execution, record reproducible provenance, and respect independent application adoption decisions. Intentional breaking changes are permitted when accompanied by documented migration paths and explicit maintainer approval.

## Motivation

Unit tests in `craft-libs` verify only that a shared crate is internally consistent. They do not demonstrate that consuming applications (such as `photocraft`, `vectorcraft`, or `lightcraft`) continue to compile and pass tests against proposed library changes.

Conversely, testing proposed changes by manually editing consumer repository configurations risks dirtying local working trees and accidentally committing unmerged dependencies. Without a standard expectation for compatibility evidence, breaking changes can land in shared crates unnoticed, creating downstream disruption when consumers update their dependency pins.

Defining required verification outcomes ensures that library updates are proven against real consumer applications while keeping tooling choices flexible and accommodating planned API evolution.

## Proposal

1. **Affected Consumer Identification**: When proposing breaking or structurally significant changes to a crate in `craft-libs`, the author must identify which applications currently depend on that crate.

2. **Isolated Verification**: Compatibility validation of candidate library revisions against consumer applications must execute in isolated environments. Testing must not modify, dirty, or leave uncommitted configuration changes in the consumer application primary working tree.

3. **Baseline Comparison and Regression Classification**: Compatibility validation must isolate the effect of the proposed shared library change by testing the identical consumer application source tree against two dependency states: the consumer's current committed dependency revision (baseline) and the proposed candidate library revision. Results must distinguish:
   - *Baseline failure*: A failure already present in the consumer application using its current committed dependency revision.
   - *Candidate regression*: A failure introduced specifically by swapping in the proposed candidate library revision.
   As a default rule, a shared library change is qualified for adoption only when it introduces zero candidate regressions in tested consumers.

4. **Intentional Breaking Changes**: Intentional breaking changes may be accepted when affected consumers are identified, the incompatibility is documented, a migration path is provided, and the responsible maintainers explicitly approve the change.

5. **Non-Vacuous Verification**: Compatibility checks must demonstrate that consumer test suites actively executed. A check that skips all comparisons, runs zero assertions, or passes vacuously due to build misconfiguration cannot be reported as valid verification. Reports must provide evidence of executed test counts.

6. **Reproducible Provenance**: Compatibility reports submitted with pull requests must record the exact commit revisions or release versions of both the candidate shared library and the tested consumer applications, allowing any maintainer or contributor to reproduce the results.

7. **Explicit and Independent Consumer Adoption**: Consuming applications adopt shared library updates through explicit pull requests within their own repositories. Applications are not required to adopt updates in lockstep. Each application maintainer determines when to update dependency pins based on compatibility evidence and application release schedules.

8. **Reference Implementation**: Tools such as `cargo xtask compat` in `craft-libs` provide one implementation of isolated testing and baseline comparison. This RFC mandates the required verification outcomes and evidence standards, rather than requiring a specific runner tool, Git index manipulation, or worktree mechanism.

## Alternatives

- **Mandate a specific tool as organization policy**: Couples ecosystem governance to a particular script or workflow mechanism, making it difficult to adapt to different CI environments or platforms.
- **Rely solely on downstream CI after merging**: Postpones regression discovery until after shared library pull requests land, forcing emergency reverts and disrupting consumer workflows.
- **Absolute zero-regression ban without exception**: Prohibits legitimate API evolution, deprecation cleanups, and major version upgrades.
- **Mandate simultaneous lockstep upgrades across all applications**: Creates cross-repository scheduling bottlenecks and prevents applications from managing their own release stability.

## Open questions

- Which consumer applications should serve as the standard qualification set for core crates such as `craft-atomic` and `craft-ui`?
- How should compatibility reports be formatted in pull request comments or automated CI checks to minimize noise while preserving provenance?

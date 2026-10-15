# RFC-0012: Shared UI presentation assessment and component reuse

Related: storytold/craft-libs#67, storytold/craft-libs#78.

## Summary

This RFC requires contributors to assess existing shared UI components in `craft-ui` before implementing reusable presentation controls in application repositories. It explicitly preserves application-specific interaction requirements, permits justified local implementations, and conditions shared component extraction on demonstrated reuse and compatibility.

## Motivation

Independent development across Craft applications has led to duplicate implementations of common presentation controls such as zoom bars, numeric scrubbers, coordinate rulers, and tab bars. While sharing generalizable presentation controls can reduce maintenance and improve accessibility, requiring every common component to move into `craft-ui` risks centralizing too much functionality and forcing unsuitable abstractions onto applications with unique workflow needs.

A CAD drafting tool, a nonlinear video timeline, and a photo editor often require different interaction densities, pointer behaviors, keyboard modifiers, or rendering performance. A balanced policy encourages reuse while protecting application autonomy.

## Proposal

1. **Existing Component Assessment**: Before introducing a new reusable presentation component, contributors must check whether an existing shared component satisfies the requirement. A brief explanation is sufficient when a local implementation is preferred.

2. **Preservation of Application-Specific Requirements**: Applications may author local presentation controls whenever:
   - Interaction model, precision, or performance requirements differ significantly from existing shared components.
   - Adopting a shared component would introduce undesirable dependencies or architectural coupling.
   - The widget is closely integrated with application domain state, document models, or unique application ergonomics.
   Contributors choosing a local implementation should document the rationale briefly in the pull request description.

3. **Conditional Extraction to `craft-ui`**: Presentation components should be proposed for extraction into `craft-ui` only when:
   - At least two applications demonstrate a clear need for the component with compatible interaction requirements.
   - The component can be cleanly decoupled from application domain state and commands.
   - The shared component provides accessible behavior (keyboard navigation, focus indicators) and theme adaptability across consuming applications.

4. **Role of UI Inventories**: Existing repository audits and UI element inventories serve as supporting evidence to identify potential collaboration opportunities. They do not constitute proof that every identified component should be shared, nor do they mandate extraction.

## Alternatives

- **Mandate that all common UI components move to craft-ui**: Centralizes too much functionality, restricts application-specific innovation, and creates a development bottleneck in the shared UI crate.
- **No cross-application UI assessment**: Leads to repeated authoring of identical controls without accessibility or theme consistency.

## Open questions

- How can `craft-ui` best provide customizable hooks and layout flexibility so applications can adapt shared controls to their specific workflows without forking?

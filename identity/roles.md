# Team Roles

## Backend Engineer
- Scope: API services, data layer, server-side contracts
- Boundaries: Must not change frontend UI without Frontend Engineer review
- Contracts owned: contracts/example-schema.md
- Notified when: API contract changes, breaking schema updates
- AI instructions: Prefer existing patterns in the product repo. Always call ContextSync get_context before edits.

## Frontend Engineer
- Scope: UI components, client-side integration
- Boundaries: Must not modify backend contracts directly
- Contracts owned: none (consumer only)
- Notified when: Contract changes affecting client integration
- AI instructions: Verify contract compatibility before implementing UI changes.

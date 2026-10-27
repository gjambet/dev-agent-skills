---
name: entity-deletion-ux
description: Design, implement, or review deletion of named domain entities and user accounts. Use when adding or changing destructive deletion controls, confirmation flows, or backend deletion endpoints in an application.
---

# Entity Deletion UX

## Presentation

- Put the deletion action in a clearly labelled danger zone on the entity's
  detail or edit page, separate from ordinary save and cancel actions. Reuse
  the application's existing danger-zone styling and terminology.
- Identify the target and explain that deletion is permanent, including
  consequential removal of related data only when verified.
- Ask the user to re-enter the target's current name. For an account, use the
  authenticated account name shown in the UI; for a domain entity, use its
  persisted name, not an unsaved edit. Show the exact expected name.
- Enable the final delete action only when the entered value exactly matches
  the expected name. Provide an accessible input label and a way to cancel.
  Clear confirmation when switching targets or reopening the flow.

## Enforcement

- Send the entered name with the deletion request. On the server, authenticate
  and authorize the caller, resolve the target by its stable ID and ownership,
  then compare the confirmation with the current authoritative name. Reject
  missing, mismatched or unavailable names before any destructive operation.
- Treat the name as confirmation, not as an identity key or an authorization
  credential. Do not accept a stale or user-supplied name as authoritative.
  Keep established permission checks and data-cleanup semantics.
- Disable repeat submission while deletion is in progress; display failures
  without reporting success, and return to an appropriate page after success.
- Test exact match, mismatch, missing input, authorization and target changes;
  verify that failed confirmation never invokes deletion. Coordinate client and
  server deployment when the request contract changes.

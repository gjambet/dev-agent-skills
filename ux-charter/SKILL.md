---
name: ux-charter
description: Design, implement, or review application breadcrumbs, footers, and deletion flows for named domain entities and user accounts. Use when changing page navigation, footer content, destructive controls, confirmation flows, or backend deletion endpoints.
---

# UX Charter

## Breadcrumbs

- Use the shared header breadcrumb on navigable pages. When adding, renaming,
  or moving a page, update its breadcrumb labels, parent trail, and routes.
- Show the contextual hierarchy from parent to current page. Use meaningful
  labels that reflect the destination, selected entity, or action. Link each
  navigable parent to its actual route and preserve the entity context needed
  to return there. Use plain text for groupings without a destination.
- Follow the application's root convention. Omit a redundant Home item when
  the app uses contextual trails and provides Home in its global navigation.
  Keep a Home link where it is an intentional parent. Avoid a duplicate Back
  control when the breadcrumb already offers the same destination.
- Render the trail as an ordered list in a navigation landmark labelled
  Breadcrumb. Mark the final, non-linked item with `aria-current="page"`.
  Keep decorative separators out of accessible names.
- Let long trails wrap or truncate within the header. Keep the current page
  identifiable and parent links usable at supported mobile widths.
- Verify the current label and parent destinations for changed routes,
  including nested detail and action pages, and check the mobile layout.

## Application footer

- Use one shared footer throughout the application. Separate it visually from
  the main content and let its contents wrap at supported mobile widths without
  overlap, clipping, or horizontal page scrolling. Omit obsolete branding.
- Include a visible `GitHub Issues` link in every application footer, including
  on public pages. Point it directly to the owning application's issue list at
  `https://github.com/<owner>/<repository>/issues`.
- Show the running image build time as `Docker build` when metadata is
  available. Show `Page generated` for server-rendered pages using the time of
  the current response. Keep that value static until the next full page request.
  Display both timestamps in ISO 8601 UTC with a `Z` suffix and whole-second precision.
- For authenticated sessions, show the current login under `User` followed by
  every active application role under `Roles`, with distinct labels or badges.
  Hide session identity for anonymous visitors.
- Use normal type for labels and role badges, and italics for timestamp and
  username values. Keep the presentation and order consistent across pages.

## Entity and account deletion

### Presentation

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

### Enforcement

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

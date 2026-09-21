---
name: keycloak-identity
description: Apply Keycloak identity architecture and migration rules. Use when onboarding a project to Keycloak, configuring realms or OIDC clients, replacing local authentication, mapping existing accounts to Keycloak identities, or reviewing identity isolation and credential storage.
---

# Keycloak Identity

Treat Keycloak as the sole authentication and credential system.

## Realm isolation

- Create one dedicated Keycloak realm for each project.
- Never share a realm between projects.
- Name the realm after the stable project identifier using lowercase kebab-case.
- Keep project users, groups, roles, clients, identity providers, authentication
  flows, required actions, email settings, and security policies in that realm.
- Create separate OIDC clients inside the realm for independently deployed
  application components when their redirect URIs, secrets, token audience, or
  security posture differ.
- Record the realm name, issuer URI, clients, redirect URIs, logout URIs, and
  role mapping in project-owned configuration or governance.

For example, the Boursicoton project uses the `boursicoton` realm, not a
shared infrastructure or Dev Workbench realm.

## Keycloak-only authentication

- Store passwords, password hashes, recovery credentials, MFA secrets, and
  authentication flows only in Keycloak.
- Do not implement or retain application-local password authentication.
- Do not add password or password-hash columns to the application database.
- Redirect interactive login, logout, password reset, account recovery, email
  verification, and MFA enrollment to Keycloak.
- Validate the token issuer, signature, audience, expiration, and intended
  client before accepting an identity.
- Keep client secrets outside source control and inject them through the
  deployment secret mechanism.

## Preserve existing application accounts

Keep the existing application account as the domain record so its data,
ownership, preferences, and history remain unchanged. Link it to Keycloak
instead of recreating or resetting it.

- Store the immutable OIDC identity as the pair `issuer` plus `sub`.
- Enforce uniqueness for the `issuer` plus `sub` pair.
- Never use email, username, or display name as the permanent identity key.
- For the first link, match an existing account by a unique normalized email
  only when Keycloak returns `email_verified=true`.
- Reject ambiguous, unverified, conflicting, or already-linked matches and
  require an explicit administrative linking workflow.
- Persist `issuer` and `sub` after the first verified link. Resolve every
  later login by that pair, even if the email changes.
- Make account linking idempotent, transactional, and auditable.
- Never create a replacement account when a valid existing account can be

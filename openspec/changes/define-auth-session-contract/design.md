## Context

`dtrpg-api` already documents token issuance through `POST /{DTRPG_API_VERSION}/auth_key`, and the current OpenAPI specification exposes `token`, `refreshToken`, and `refreshTokenTTL`. What is still missing is a child proposal that makes this repository's ownership explicit within the broader auth/session rollout pattern introduced in the top-level meta-repository.

## Goals / Non-Goals

**Goals:**
- Show how a child proposal in `dtrpg-api` hangs off the top-level auth/session umbrella change.
- Define which auth/session concerns are contract-owned by the API repository.
- Provide a stable dependency point for future SDK and app child proposals.

**Non-Goals:**
- Change the current HTTP endpoints in this example proposal
- Define SDK retry, refresh, or caching behavior
- Define application sign-in or session recovery UX

## Decisions

Create a dedicated `auth-session-contract` capability in `dtrpg-api`.
Rationale: token issuance, refresh semantics, expiry meaning, and auth-failure contract are API responsibilities and should be discoverable as a cohesive contract surface.

Modify `auth-token-exchange` instead of replacing it.
Rationale: token exchange already exists as a capability, and the child proposal should show how a repository refines an existing stable spec while adding a new adjacent one.

Modify `api-error-contract` to explicitly cover auth/session failures.
Rationale: SDKs and applications need a stable source of truth for how auth-related failures are represented before they can map those failures into language or UX behavior.

## Risks / Trade-offs

- The proposal is more structural than functional right now -> Mitigation: keep the example focused on ownership and dependency, then evolve it with concrete endpoint changes later.
- Current docs and OpenAPI content may not yet cover every auth/session path implied here -> Mitigation: treat this child proposal as the place where those future contract details must be specified.
- SDK and app repos could still implement assumptions before the API contract is sharpened -> Mitigation: use this child proposal as the explicit contract dependency for downstream auth/session work.

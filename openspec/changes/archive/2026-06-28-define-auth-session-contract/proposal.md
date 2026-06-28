## Why

The top-level `dtrpg` repo now contains an umbrella auth/session rollout example, but the API layer still needs its own child proposal that states what contract details belong in `dtrpg-api`. Without that child proposal, the repo family still lacks a concrete example of how top-level coordination turns into API-owned work.

## What Changes

- Clarify that `dtrpg-api` owns the HTTP contract for token issuance, refresh semantics, token expiry meaning, and auth-related failure behavior.
- Define the API-side contract expectations that downstream SDK and app proposals should depend on.
- Record that this proposal is a child of the top-level `improve-auth-session-lifecycle` umbrella change.
- Strengthen the auth and error capabilities so future auth/session work starts from a documented API contract.

## Capabilities

### New Capabilities
- `auth-session-contract`: Defines the API-owned token, refresh, expiry, and auth-failure semantics that child repos consume.

### Modified Capabilities
- `auth-token-exchange`: Clarifies that token issuance behavior includes lifecycle semantics that downstream repos depend on.
- `api-error-contract`: Clarifies that auth/session failures use API-defined error semantics before SDKs and apps adapt them.

## Impact

- `dtrpg-api/openspec`: New child capability for auth/session contract ownership
- `openapi.yaml`: Future contract work for auth/session endpoints and responses
- Downstream SDK and app repos: Consumers of the API auth/session contract defined here
- Parent initiative: `dtrpg/openspec/changes/improve-auth-session-lifecycle`

## 1. API Contract Specs

- [x] 1.1 Add the `auth-session-contract` delta spec in `dtrpg-api`
- [x] 1.2 Update `auth-token-exchange` to emphasize API ownership of token lifecycle semantics
- [x] 1.3 Update `api-error-contract` to cover auth/session failure semantics

## 2. Parent-Child Alignment

- [x] 2.1 Reference the top-level `improve-auth-session-lifecycle` umbrella change in the child proposal context
- [x] 2.2 Confirm the API contract changes are sequenced ahead of downstream SDK and app child proposals

## 3. Future Contract Follow-Through

- [x] 3.1 Translate approved auth/session contract changes into `openapi.yaml`
- [x] 3.2 Validate that downstream SDK and app proposals rely on the API-defined contract rather than restating it

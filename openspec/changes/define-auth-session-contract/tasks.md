## 1. API Contract Specs

- [ ] 1.1 Add the `auth-session-contract` delta spec in `dtrpg-api`
- [ ] 1.2 Update `auth-token-exchange` to emphasize API ownership of token lifecycle semantics
- [ ] 1.3 Update `api-error-contract` to cover auth/session failure semantics

## 2. Parent-Child Alignment

- [ ] 2.1 Reference the top-level `improve-auth-session-lifecycle` umbrella change in the child proposal context
- [ ] 2.2 Confirm the API contract changes are sequenced ahead of downstream SDK and app child proposals

## 3. Future Contract Follow-Through

- [ ] 3.1 Translate approved auth/session contract changes into `openapi.yaml`
- [ ] 3.2 Validate that downstream SDK and app proposals rely on the API-defined contract rather than restating it

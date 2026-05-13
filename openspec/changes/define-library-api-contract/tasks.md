## 1. API Contract Specs

- [x] 1.1 Add the `library-resource-contract` delta spec in `dtrpg-api`
- [x] 1.2 Add the `library-pagination-contract` delta spec in `dtrpg-api`
- [ ] 1.3 Update `order-products-listing` to reference `library-pagination-contract` as a formal pagination dependency

## 2. Parent-Child Alignment

- [x] 2.1 Reference the top-level `add-library-api` umbrella change in the child proposal context
- [x] 2.2 Confirm the API contract changes are sequenced ahead of downstream SDK and app child proposals

## 3. Future Contract Follow-Through

- [ ] 3.1 Refine the `prepare` endpoint response schema in `openapi.yaml` and update `library-resource-contract` to reflect the stable shape
- [ ] 3.2 Validate that downstream SDK and app proposals derive library resource types from the API-defined contracts rather than restating them independently

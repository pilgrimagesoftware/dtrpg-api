## Why

The `order-products-listing` stable spec already covers the paginated product list endpoint, but the rest of the library API surface — ordered product detail, download preparation, product list collections, and product list items — has no formal contract ownership. Without it, SDK implementors must infer behavior from `openapi.yaml` examples rather than a documented, capability-owned contract. This child proposal establishes `dtrpg-api` as the explicit source of truth for those resource shapes and for the shared pagination model that all library endpoints rely on.

## What Changes

- Define a new `library-resource-contract` capability that owns the HTTP contract for the ordered product detail endpoint, the download preparation endpoint, the product list collection endpoint, and the product list items endpoint.
- Define a new `library-pagination-contract` capability that formalizes the shared `PaginationLinks` and `PaginationMeta` pagination model used across all paginated library endpoints.
- Record that the existing `order-products-listing` capability will eventually reference `library-pagination-contract` as a dependency, so the pagination contract is sourced from one place.
- Record that this proposal is a child of the top-level `add-library-api` umbrella change.

## Capabilities

### New Capabilities
- `library-resource-contract`: Owns the API contract for ordered product detail, download preparation, product list collections, and product list items.
- `library-pagination-contract`: Owns the shared `PaginationLinks` and `PaginationMeta` model that all paginated library responses share.

### Modified Capabilities
- `order-products-listing`: Will reference the new `library-pagination-contract` as a formal pagination dependency once that capability is stable.

## Impact

- `dtrpg-api/openspec`: Two new child capabilities for library resource and pagination contract ownership
- `openapi.yaml`: Future contract refinement work for library resource endpoints and their response schemas
- Downstream SDK and app repos: Consumers of the library resource and pagination contracts defined here
- Parent initiative: `dtrpg/openspec/changes/add-library-api`

## Context

`dtrpg-api` already documents the full library API surface in `openapi.yaml` and has a stable `order-products-listing` spec that covers the paginated product list endpoint. What is still missing is formal contract ownership for the remaining library endpoints — ordered product detail, download preparation, product list collections, and product list items — and for the shared pagination model that all library responses use. Without that ownership, SDK maintainers have no stable capability to depend on when implementing types and deserialization for those resources.

The `prepare` endpoint (`GET /{version}/order_products/{orderProductId}/prepare`) is currently typed as a generic object in `openapi.yaml`. Its response shape has not been finalized, so it requires special treatment: this change records its existence under the resource contract but explicitly marks it as not yet a stable contract surface.

## Goals / Non-Goals

**Goals:**
- Establish formal contract ownership for all library endpoints that are not yet covered by a capability spec.
- Provide a stable dependency point for downstream SDK and application repositories implementing library resource types.
- Extract the shared pagination model into a reusable `library-pagination-contract` capability that all library endpoints — including the existing `order-products-listing` — can reference.

**Non-Goals:**
- Change the current HTTP endpoint paths or query parameter surface.
- Define SDK-level retry logic, caching behavior, or download management strategies.
- Define application UX for library browsing or download flows.

## Decisions

Create a dedicated `library-resource-contract` capability in `dtrpg-api`.
Rationale: the ordered product detail, download preparation, product list collection, and product list items endpoints share a common concern — library resource ownership — but are distinct enough from the listing endpoint to warrant a separate capability. Grouping them here keeps the listing contract stable while adding ownership for the rest of the surface.

Create a dedicated `library-pagination-contract` capability as a standalone spec.
Rationale: the same `PaginationLinks` and `PaginationMeta` structures appear in every paginated library response. Extracting them into their own capability means SDK implementors can depend on one pagination contract rather than inferring it separately from each endpoint. The existing `order-products-listing` spec will reference this capability as a dependency once it is stable.

Treat the `prepare` endpoint response as intentionally unspecified for now.
Rationale: the current `openapi.yaml` types the prepare response as a generic object, reflecting the fact that the response shape is not yet finalized. Recording this explicitly in the resource contract prevents SDK repos from treating the prepare response as stable and building strongly-typed deserialization before the API contract is ready.

## Risks / Trade-offs

- The `prepare` endpoint response is under-specified, which means SDK implementors may make local assumptions about its shape. Mitigation: the `library-resource-contract` spec explicitly marks the prepare response as not a stable contract, giving SDK maintainers a documented reason to keep deserialization loose until the API repository publishes a formal schema.
- SDK repositories could implement their own pagination structures without referencing the `library-pagination-contract` capability. Mitigation: this child proposal is the explicit contract dependency for pagination across all library endpoints, and downstream SDK child proposals should reference it before stabilizing pagination types.
- This change is primarily structural rather than functional, recording ownership rather than changing behavior. Mitigation: the value is the stable capability surface it creates; concrete endpoint refinements will follow as separate changes once the contracts are established.

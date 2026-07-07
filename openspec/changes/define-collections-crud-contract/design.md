## Context

Captured live traffic (request/response pairs) shows the DriveThruRPG API already supports four undocumented operations:

- `POST /product_lists` — create a collection, body `{ "name": string }`, returns `201` with the full `ProductListAttributes` shape (customerId, name, dateCreated, productListId, slug, itemCount).
- `DELETE /product_lists/{productListId}` — delete a collection, returns `204 No Content`.
- `POST /product_list_items` — add an item to a collection, body `{ "productId": integer, "productListId": integer }`, returns `201` with `{ productId, productListId, productListItemId }`.
- `DELETE /product_list_items/{productListItemId}` — remove an item from a collection, returns `204 No Content`.

These four operations complete the CRUD surface for collections; `GET /product_lists` and `GET /product_list_items` are already contracted.

## Goals / Non-Goals

**Goals:**
- Contract the four create/delete operations in `openapi.yaml`, matching the captured request/response shapes exactly.
- Reuse the existing `ProductListAttributes` schema for the create-collection response rather than duplicating it.
- Define a new schema for the create-item response, since no existing schema covers a single `product_list_item` resource.

**Non-Goals:**
- No pagination, filtering, or bulk operations for these endpoints — the captured traffic doesn't show them and they're out of scope.
- No SDK implementation — this change only contracts the API repository.

## Decisions

- **Reuse `ProductListAttributes` for the create response**: the captured `201` body for `POST /product_lists` matches the existing schema's fields exactly, so no new schema is introduced.
- **New `ProductListItemCreateResponse` schema**: the create-item response (`productId`, `productListId`, `productListItemId`) doesn't match any existing schema (the GET items endpoint uses an untyped `PaginatedResponse`), so a minimal dedicated schema is added.
- **Path parameters for delete operations**: `productListId` and `productListItemId` are path parameters, matching the captured `DELETE /product_lists/86150` and `DELETE /product_list_items/2629322` requests.
- **`204 No Content` for both delete operations**: matches captured responses; no response body schema is defined for these.
- **Reuse `AuthSessionError` for the `default` response**: consistent with every other authenticated endpoint already in the spec.

## Risks / Trade-offs

- [Captured traffic reflects one account/session, so edge cases like duplicate collection names or invalid `productId` aren't documented] → Contract only the observed success and generic-failure shapes; downstream SDKs treat `default` as the catch-all until more error cases are captured.

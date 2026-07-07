## Why

The OpenAPI spec currently defines only read access to collections (`GET /product_lists`, `GET /product_list_items`). Captured request/response traffic shows the live API also supports creating and deleting collections, and adding and removing items within a collection. Those endpoints are undocumented, so SDKs and applications have no contracted shape to implement against.

## What Changes

- Add `POST /{DTRPG_API_VERSION}/product_lists` to create a collection, returning the created `ProductListAttributes` payload.
- Add `DELETE /{DTRPG_API_VERSION}/product_lists/{productListId}` to delete a collection, returning `204 No Content`.
- Add `POST /{DTRPG_API_VERSION}/product_list_items` to add an item to a collection, returning the created item's identifiers.
- Add `DELETE /{DTRPG_API_VERSION}/product_list_items/{productListItemId}` to remove an item from a collection, returning `204 No Content`.

## Capabilities

### New Capabilities
- `collections-crud-contract`: Defines the request/response contract for creating and deleting collections, and adding and removing items within a collection.

### Modified Capabilities

## Impact

- `openapi.yaml`: adds four new operations and their request/response schemas.
- Downstream SDKs (Go, Python, Rust, Swift) will need to implement collection create/delete and item add/remove once this contract lands.

## 1. Schemas

- [x] 1.1 Add `ProductListItemCreateResponse` schema (`productId`, `productListId`, `productListItemId`) to `openapi.yaml` components
- [x] 1.2 Confirm `ProductListAttributes` covers the `POST /product_lists` response body with no changes needed

## 2. Collection endpoints

- [x] 2.1 Add `POST /{DTRPG_API_VERSION}/product_lists` operation: request body schema (`name`), `201` response using `ProductListAttributes`, `default` error using `AuthSessionError`
- [x] 2.2 Add `DELETE /{DTRPG_API_VERSION}/product_lists/{productListId}` operation: path parameter, `204` response, `default` error using `AuthSessionError`

## 3. Collection item endpoints

- [x] 3.1 Add `POST /{DTRPG_API_VERSION}/product_list_items` operation: request body schema (`productId`, `productListId`), `201` response using `ProductListItemCreateResponse`, `default` error using `AuthSessionError`
- [x] 3.2 Add `DELETE /{DTRPG_API_VERSION}/product_list_items/{productListItemId}` operation: path parameter, `204` response, `default` error using `AuthSessionError`

## 4. Validation

- [x] 4.1 Validate `openapi.yaml` against the OpenAPI 3.0 schema
- [x] 4.2 Cross-check each new operation's example values against the captured request/response files in `dtrpg-collection-*-req-resp.folder/`

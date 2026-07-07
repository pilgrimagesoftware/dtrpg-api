# collections-crud-contract Specification

## Purpose
Define the API repository as the source of truth for creating and deleting collections (product lists) and for adding and removing items within a collection, so SDKs and applications implement these mutations against a contracted shape rather than inferring them from captured traffic.

## Requirements

### Requirement: The API repository MUST define the contract for creating a collection
The API repository MUST define the request and response shape for `POST /{DTRPG_API_VERSION}/product_lists`. The request body SHALL contain a `name` string. On success, the API SHALL return `201 Created` with the created collection's `customerId`, `name`, `dateCreated`, `productListId`, `slug`, and `itemCount`.

#### Scenario: Creating a new collection
- **WHEN** a client sends `POST /product_lists` with body `{ "name": "Maps" }`
- **THEN** the API returns `201 Created` with a body containing `customerId`, `name`, `dateCreated`, `productListId`, `slug`, and `itemCount`

### Requirement: The API repository MUST define the contract for deleting a collection
The API repository MUST define the request and response shape for `DELETE /{DTRPG_API_VERSION}/product_lists/{productListId}`. On success, the API SHALL return `204 No Content`.

#### Scenario: Deleting an existing collection
- **WHEN** a client sends `DELETE /product_lists/{productListId}` for a collection owned by the authenticated user
- **THEN** the API returns `204 No Content` with no response body

### Requirement: The API repository MUST define the contract for adding an item to a collection
The API repository MUST define the request and response shape for `POST /{DTRPG_API_VERSION}/product_list_items`. The request body SHALL contain `productId` and `productListId` integers. On success, the API SHALL return `201 Created` with `productId`, `productListId`, and the newly assigned `productListItemId`.

#### Scenario: Adding a product to a collection
- **WHEN** a client sends `POST /product_list_items` with body `{ "productId": 515276, "productListId": 86151 }`
- **THEN** the API returns `201 Created` with a body containing `productId`, `productListId`, and `productListItemId`

### Requirement: The API repository MUST define the contract for removing an item from a collection
The API repository MUST define the request and response shape for `DELETE /{DTRPG_API_VERSION}/product_list_items/{productListItemId}`. On success, the API SHALL return `204 No Content`.

#### Scenario: Removing a product from a collection
- **WHEN** a client sends `DELETE /product_list_items/{productListItemId}` for an item owned by the authenticated user
- **THEN** the API returns `204 No Content` with no response body

### Requirement: Collection create/delete endpoints MUST require authentication
All four collection and collection-item mutation endpoints MUST require a valid Bearer token, consistent with the existing `GET /product_lists` and `GET /product_list_items` endpoints.

#### Scenario: Requesting collection mutation without a valid token
- **WHEN** a client sends a create, delete, add-item, or remove-item request without a valid Bearer token
- **THEN** the API returns the API-defined auth/session failure response

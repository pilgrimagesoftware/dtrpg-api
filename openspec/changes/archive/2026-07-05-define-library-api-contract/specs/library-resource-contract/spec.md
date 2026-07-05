## ADDED Requirements

### Requirement: The API repository MUST own the contract for library resource detail endpoints
The API repository MUST define the response shape, required fields, and error behavior for the ordered product detail endpoint, the download preparation endpoint, the product list collection endpoint, and the product list items endpoint.

#### Scenario: Locating the source of truth for library resource shapes
- **WHEN** SDK or application maintainers need the authoritative definition of an ordered product, product list, or product list items response
- **THEN** the API repository is the source of truth for those resource shapes

### Requirement: Library resource contracts MUST precede downstream SDK implementation
Changes to library resource shapes MUST be specified in the API repository before SDK repositories treat those shapes as stable dependencies.

#### Scenario: Planning Rust SDK library implementation
- **WHEN** the Rust SDK defines types for ordered products, product lists, or product list items
- **THEN** those types are derived from the API-defined resource contract rather than inferred from examples

### Requirement: The prepare-download endpoint response MUST be explicitly contracted before SDKs serialize it
The `GET /order_products/{id}/prepare` endpoint response shape MUST be formally defined in the API repository before downstream SDKs implement strongly-typed deserialization for it.

#### Scenario: Implementing download preparation in the Rust SDK
- **WHEN** the Rust SDK implements download preparation
- **THEN** the SDK treats the prepare response as an untyped or partially-typed payload until the API repository provides a formal schema contract

## ADDED Requirements

### Requirement: The API repository MUST own the pagination model used across all library endpoints
The API repository MUST define the `PaginationLinks` and `PaginationMeta` structures that all paginated library responses share, so SDKs can implement pagination behavior from a single, stable source.

#### Scenario: Implementing pagination in the Rust SDK
- **WHEN** the Rust SDK implements support for a paginated library endpoint
- **THEN** it uses the pagination model defined by the API repository rather than defining its own pagination structure

### Requirement: Paginated library responses MUST include both links and metadata
Every paginated library API response MUST include a `links` object (with at minimum a `self` URL) and a `meta` object (with `itemsPerPage` and `currentPage`) so SDK and application consumers can navigate pages deterministically.

#### Scenario: Navigating pages of ordered products
- **WHEN** a caller requests a page of ordered products, product lists, or product list items
- **THEN** the response includes `links.self` and the `meta.itemsPerPage`/`meta.currentPage` fields as defined in the API pagination contract

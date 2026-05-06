# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## About This Project

This repository contains the **OpenAPI specification** for the DriveThruRPG API. It serves as the single source of truth for API documentation and is used by all language-specific SDK implementations (Go, Python, Rust, Swift) to generate client code.

## Repository Structure

- `openapi.yaml` - OpenAPI 3.0 specification defining the DriveThruRPG API
- `README.md` - Basic repository description

## OpenAPI Specification

The `openapi.yaml` file defines:
- **Base URL**: `https://api.drivethrurpg.com/api`
- **Authentication**: API key-based (applicationKey query parameter)
- **Version**: Path parameter `DTRPG_API_VERSION` (e.g., `vBeta`)

### Current Endpoints

1. **POST /{DTRPG_API_VERSION}/auth_key** - Exchange application key for JWT authentication token
   - Returns: `token`, `refreshToken`, `refreshTokenTTL`
   - Uses applicationKey from environment variable

2. **GET /{DTRPG_API_VERSION}/order_products** - Retrieve user's product library
   - Query parameters: `getChecksum`, `getFilters`, `page`, `pageSize`, `library`, `archived`, `updatedDate[after]`
   - Requires: Authorization header with JWT token

## Modifying the API Specification

When making changes to the OpenAPI specification:

1. Edit `openapi.yaml` following OpenAPI 3.0 standards
2. Test the specification validity (use online validators or tools)
3. Commit and push changes to this repository
4. Update the submodule reference in any parent repositories (e.g., `dtrpg-sdk`)
5. Language-specific SDKs will regenerate their client code on next build

## Important Notes

- This repository is used as a **git submodule** in multiple SDK repositories
- Changes here affect ALL language implementations
- The OpenAPI specification should remain language-agnostic
- Example values in the spec may contain real JWT tokens for reference but should not be treated as valid credentials

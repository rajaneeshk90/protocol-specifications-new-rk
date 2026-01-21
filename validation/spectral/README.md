# Spectral Validation for Beckn Protocol 2.0

This directory contains Spectral configuration for validating OpenAPI specifications against Beckn Protocol 2.0 style guidelines.

## What is Spectral?

[Spectral](https://stoplight.io/open-source/spectral) is an open-source JSON/YAML linter created by Stoplight. It is the industry-standard tool for validating OpenAPI and JSON Schema files.

**Key features:**
- Validates OpenAPI 2.0, 3.0, and 3.1 specifications
- Supports custom rules via YAML configuration
- Provides detailed error messages with line numbers
- Integrates easily with CI/CD pipelines
- Extensible with JavaScript functions for complex validations

**Why we use it:**
- Purpose-built for OpenAPI validation
- Declarative rules are easy to read and maintain
- Strong community support and documentation
- Native integration with GitHub Actions

We're using the Spectral CLI (`@stoplight/spectral-cli`) which is a Node.js package.

## Prerequisites

Before running validation, ensure you have the following installed:

| Dependency | Version | Installation |
|------------|---------|--------------|
| Node.js | >= 18.0.0 | [nodejs.org](https://nodejs.org/) or via nvm: `nvm install 18` |
| npm | >= 8.0.0 | Included with Node.js |

**Verify installation:**
```bash
node --version   # Should show v18.x.x or higher
npm --version    # Should show 8.x.x or higher
```

## Quick Start

```bash
# Navigate to this directory
cd validation/spectral

# Install dependencies (includes Spectral)
npm install

# Run validation
npm run lint
```

> **Note:** Spectral is installed automatically as a local dependency. No global installation required.

## What It Validates

| Rule | Severity | Description |
|------|----------|-------------|
| `path-snake-case` | Error | API endpoint paths must use snake_case |
| `property-camel-case` | Warning | Property names must use camelCase |
| `enum-screaming-snake-case` | Warning | Enum values must use SCREAMING_SNAKE_CASE |
| `schema-pascal-case` | Warning | Schema/class names must use PascalCase |

## Files Validated

- `api/beckn.yaml` - Main API specification
- `schema/core/v2/attributes.yaml` - Core schema definitions
- `schema/*/v1/attributes.yaml` - Domain-specific schemas (EV Charging, Payment Settlement)

## Available Commands

```bash
# Lint all files
npm run lint

# Lint only API spec
npm run lint:api

# Lint only schema files
npm run lint:schemas
```

## Known Exceptions

The rules allow certain patterns that are valid in Beckn:

### Property Names (camelCase)
- `@context`, `@type`, `@id` - JSON-LD properties
- `beckn:*`, `schema:*` - Namespaced properties

### Enum Values (SCREAMING_SNAKE_CASE)
- `text/html`, `application/json` - MIME types
- `https://...` - URLs
- `CCS2`, `Type2`, `CHAdeMO` - Industry standard codes
- `beckn:Form`, `schema:Thing` - JSON-LD type references

## CI/CD Integration

This validation runs automatically via GitHub Actions on:
- Pull requests to `main`/`master`
- Pushes to `main`/`master`

See `.github/workflows/validate-style.yml` for the workflow configuration.

## Customizing Rules

Edit `.spectral.yaml` to:
- Change severity levels (`error`, `warn`, `info`, `hint`, `off`)
- Add new rules
- Modify regex patterns for exceptions

## Troubleshooting

**Warnings from remote URLs:**
Some warnings may appear from remote schema references (e.g., `https://raw.githubusercontent.com/...`). These are from external schemas, not local files.

**False positives:**
If a valid pattern is flagged, check if it needs to be added to the exception regex in `.spectral.yaml`.


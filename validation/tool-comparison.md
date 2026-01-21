# Beckn Protocol 2.0 - Validation Tool Comparison

## Overview

This document compares validation tools for enforcing Beckn Protocol 2.0 style guidelines across different file types.

---

## Tools Evaluated

### 1. Shell Script

**What it is:** Bash scripts using `grep`, `sed`, `awk` for pattern matching.

**Pros:**
- No dependencies required
- Simple for basic pattern matching
- Universal availability

**Cons:**
- Cannot reliably parse YAML/JSON structure
- High false positive rate (matches in comments, strings, descriptions)
- Difficult to maintain exclusion lists
- Cannot distinguish context (property name vs schema name vs description)
- Complex regex patterns become unreadable
- Poor error messages

**Best for:** Not recommended for Beckn validation

---

### 2. Spectral

**What it is:** Industry-standard OpenAPI/JSON Schema linter with declarative YAML rules.

**Pros:**
- Purpose-built for OpenAPI validation
- Excellent error messages with line numbers
- Declarative rules (easy to read and maintain)
- Native GitHub Actions integration
- Large community and ecosystem

**Cons:**
- Limited to OpenAPI/JSON Schema files
- Cannot validate JSON-LD, profile.json, or README files
- Cannot perform cross-file consistency checks

**Best for:** `api/beckn.yaml`, `schema/*/attributes.yaml`

---

### 3. Node.js

**What it is:** Custom JavaScript/TypeScript validation scripts using libraries like `js-yaml`, `ajv`, etc.

**Pros:**
- Full programmatic control
- Can validate any file type (YAML, JSON, JSON-LD, Markdown)
- Can perform cross-file consistency checks
- Easy to handle complex exclusion logic
- Customizable error messages

**Cons:**
- Requires writing and maintaining custom code
- No built-in OpenAPI awareness (would need to parse manually)
- More setup than declarative tools

**Best for:** JSON-LD files, `profile.json`, cross-file validation, complex business rules

---

## Rule Coverage

| Validation Rule | Shell | Spectral | Node.js |
|-----------------|-------|----------|---------|
| Property names must use camelCase | ⚠️ Limited | ✅ Good | ✅ Best |
| Enum values must use SCREAMING_SNAKE_CASE | ⚠️ Limited | ✅ Good | ✅ Best |
| Schema names must use PascalCase with domain prefix | ⚠️ Limited | ✅ Good | ✅ Best |
| Endpoint paths must use snake_case | ✅ Good | ✅ Best | ✅ Good |
| No typos in descriptions | ❌ No | ❌ No | ✅ Best* |
| JSON-LD vocabulary consistency | ❌ No | ❌ No | ✅ Best |
| Cross-file reference validation | ❌ No | ❌ No | ✅ Best |
| Example values match enum definitions | ❌ No | ⚠️ Limited | ✅ Best |

*\* Requires libraries like `cspell`, `retext`, or `textlint`*

---

## Recommendation

**Spectral + Node.js (Hybrid Approach)**

| Validation Rule | Recommended Tool |
|-----------------|------------------|
| Property names must use camelCase | Spectral |
| Enum values must use SCREAMING_SNAKE_CASE | Spectral |
| Schema names must use PascalCase with domain prefix | Spectral |
| Endpoint paths must use snake_case | Spectral |
| No typos in descriptions | Node.js |
| JSON-LD vocabulary consistency | Node.js |
| Cross-file reference validation | Node.js |
| Example values match enum definitions | Node.js |

**Why not Shell?**

Shell scripts were initially considered but rejected because:
1. Cannot reliably parse YAML/JSON structure
2. High false positive rate with regex-based matching
3. Hard to maintain lists of valid exceptions
4. Cannot distinguish between property names, schema names, and descriptions
5. Complex regex patterns become unreadable over time


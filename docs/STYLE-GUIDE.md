# Beckn Protocol 2.0 - Spec Authoring Style Guide

This document defines the naming conventions and standards for authoring Beckn Protocol 2.0 specifications. Follow these guidelines to maintain consistency across schemas, APIs, and documentation.

---

## 1. Property Naming

### Convention: **camelCase**

All property names must use camelCase.

```yaml
# ✅ Correct
transactionId: "abc-123"
textSearch: "gaming laptop"
maxItemsPerPage: 100

# ❌ Incorrect
transaction_id: "abc-123"
text_search: "gaming laptop"
max_items_per_page: 100
```

### Exception: Context Object

Context object properties (`message_id`, `bap_id`, `bap_uri`, `bpp_id`, `bpp_uri`) remain in snake_case for backward compatibility with Beckn 1.x.

---

## 2. Enum Values

### Convention: **SCREAMING_SNAKE_CASE**

All enum values must use SCREAMING_SNAKE_CASE.

```yaml
# ✅ Correct
enum: [ACTIVE, PENDING, COMPLETED, ON_HOLD]
enum: [HTTP_GET, HTTP_POST, WS_HANDLE]
enum: [S_WITHIN, S_CONTAINS, S_INTERSECTS]

# ❌ Incorrect
enum: [active, pending, completed]
enum: [http/get, http/post]
enum: [s_within, s_contains]
enum: [OnStreet, OffStreet]
```

### Exception: Industry Standard Identifiers

Values that are industry standards may retain their original casing:

```yaml
# ✅ Acceptable (industry standards)
connectorType:
  enum: [CCS2, Type2, CHAdeMO, GB_T]
```

---

## 3. Schema/Class Naming

### Convention: **PascalCase with Domain Prefix**

Schema class names must:
- Use PascalCase
- Match their folder name exactly
- Include domain prefix for domain-specific schemas

```yaml
# ✅ Correct
# Folder: schema/EvChargingService/v1/
EvChargingService:
  properties:
    "@type": EvChargingService

# ❌ Incorrect
# Folder: schema/EvChargingService/v1/
ChargingService:  # Missing "Ev" prefix
  properties:
    "@type": ChargingService
```

### Core vs Domain Schemas

| Type | Naming | Example |
|------|--------|---------|
| Core (reusable) | No prefix | `Catalog`, `Item`, `Offer`, `Provider` |
| Domain-specific | Domain prefix | `EvChargingService`, `EvChargingOffer` |

---

## 4. API Endpoint Naming

### Convention: **snake_case for paths**

Endpoint path segments use snake_case.

```yaml
# ✅ Correct
/beckn/discover/browser_search
/beckn/on_discover

# ❌ Incorrect
/beckn/discover/browser-search  # hyphen
/beckn/discover/browserSearch   # camelCase
```

### Action Names in Context

Action names in `context.action` use snake_case to match endpoint naming:

```yaml
# ✅ Correct
context:
  action: "discover"
  # or for compound actions:
  action: "on_discover"
```

---

## 5. Abbreviations & Units

### Convention: **Uppercase abbreviations**

Abbreviations and unit suffixes use uppercase.

```yaml
# ✅ Correct
paymentURL: "https://..."
maxPowerKW: 60
meteredEnergyKWH: 18.9

# ❌ Incorrect
paymentUrl: "https://..."
maxPowerKw: 60
meteredEnergyKWh: 18.9
```

---

## 6. JSON-LD Files

### vocab.jsonld

- `@id`: Use `beckn:` prefix with PascalCase class name
- `rdfs:label`: Human-readable with spaces
- `schema:identifier`: Match enum value exactly

```json
{
  "@id": "beckn:EvChargingService",
  "rdfs:label": "EV Charging Service",
  "schema:identifier": "EvChargingService"
}
```

### context.jsonld

- Map class/property names to their `beckn:` equivalents

```json
{
  "@context": {
    "EvChargingService": "beckn:EvChargingService",
    "connectorType": "beckn:connectorType"
  }
}
```

### alternateName (Optional)

Use `schema:alternateName` only for meaningful alternatives:
- ✅ Common variations: `["Wi-Fi", "WiFi"]`
- ✅ Spelling variants: `"CANCELED"` (US) for `"CANCELLED"` (UK)
- ✅ Abbreviations: `"SOC"` for `"STATE_OF_CHARGE"`
- ❌ Mechanical conversions: Don't add `"PER-KWH"` just because canonical is `"PER_KWH"`

---

## 7. Examples

### Convention: Examples must match schema definitions

Example values must exactly match their enum definitions.

```yaml
# Schema
trackingStatus:
  type: string
  enum: [ACTIVE, DISABLED, COMPLETED]

# ✅ Correct example
example:
  trackingStatus: "ACTIVE"

# ❌ Incorrect example
example:
  trackingStatus: "active"  # wrong casing
```

---

## 8. Documentation

### Grammar & Spelling

- Use correct grammar and spelling in all descriptions
- Use American English spelling (e.g., "color" not "colour")

### Markdown Formatting

- Use proper bold syntax: `**text**` not `**text` or `text**`
- Add space after punctuation: `i.e., ` not `i.e.`
- Ensure table formatting is consistent

### Schema References

- Always reference the correct schema name as defined in the spec
- Keep documentation in sync with actual schema definitions

---

## 9. File Organization

### Folder Structure

```
schema/
├── core/v2/
│   ├── attributes.yaml
│   ├── vocab.jsonld
│   └── context.jsonld
├── EvChargingService/v1/
│   ├── attributes.yaml
│   ├── vocab.jsonld
│   ├── context.jsonld
│   ├── profile.json
│   ├── README.md
│   └── examples/
└── ...
```

### Naming Alignment

| Artifact | Naming Must Match |
|----------|-------------------|
| Folder name | Schema class name |
| `@id` in vocab.jsonld | Schema class name |
| `@type` in attributes.yaml | Schema class name |
| References in README | Schema class name |

---

## Quick Reference

| Element | Convention | Example |
|---------|------------|---------|
| Properties | camelCase | `transactionId`, `textSearch` |
| Enum values | SCREAMING_SNAKE_CASE | `ACTIVE`, `ON_STREET`, `HTTP_GET` |
| Schema classes | PascalCase | `EvChargingService`, `Catalog` |
| API paths | snake_case | `/on_discover`, `/browser_search` |
| Abbreviations | UPPERCASE | `URL`, `KW`, `KWH` |

---

## Checklist for New Schemas

- [ ] Class name matches folder name
- [ ] All properties use camelCase
- [ ] All enum values use SCREAMING_SNAKE_CASE
- [ ] Examples match enum definitions exactly
- [ ] vocab.jsonld `@id` matches class name
- [ ] context.jsonld mappings are correct
- [ ] README references correct schema names
- [ ] No typos or grammar errors in descriptions


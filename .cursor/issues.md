# Beckn Protocol 2.0 Naming Inconsistencies & Style Guide Proposal

## Summary

Across `api/beckn.yaml` and the schema bundles under `schema/` (OpenAPI schemas + JSON-LD context/vocab + profile JSON + READMEs), there are multiple naming inconsistencies and semantic ambiguities in:

- endpoint paths and action/callback pairing
- schema/class names (domain-agnostic vs domain-specific)
- property names (reserved words like `type`, casing drift, acronym casing, tautologies)
- examples and docs (values not matching enums, documentation referring to non-existent schema names)
- cross-artifact naming drift (OpenAPI vs JSON-LD vs README vs profile JSON)

These inconsistencies make it hard for spec authors to extend Beckn Protocol 2.0 predictably and increase the chance of incompatible or awkward schema evolution.

This issue proposes the need for a **Beckn Protocol 2.0 spec-authoring style guide** (inspired by schema.org's style guide) to define conventions for:

- endpoint naming (action vs meta endpoints, callback naming, path token rules)
- schema/class naming (domain-agnostic vs domain-specific, action schemas)
- property naming (grammar, avoiding ambiguous fields like `type`, casing rules, avoiding tautologies)
- editorial quality (grammar, consistent terminology)
- ensuring consistency between OpenAPI schema, JSON-LD vocab/context, profiles, and documentation

> **Note:** This issue intentionally does not propose renames or the final naming convention yet. It only documents anomalies and motivates the creation of the style guide.

---

## Scope

**Artifacts reviewed:**

- **API:** `api/beckn.yaml`
- **Core schemas:** `schema/core/v2/attributes.yaml` (+ JSON-LD context/vocab)
- **Domain bundles:** EV charging + Payment Settlement
  - `schema/*/v1/attributes.yaml`
  - `schema/*/v1/context.jsonld`
  - `schema/*/v1/vocab.jsonld`
  - `schema/EvChargingService/v1/profile.json`
  - `schema/*/v1/README.md`

---

## A) API Endpoint Naming Anomalies (`api/beckn.yaml`)

### A1. Hyphenated endpoint path segment

- **Where:** `api/beckn.yaml` → `paths./beckn/discover/browser-search`
- **Anomaly:** `browser-search` uses a hyphen.
- **Why it's an issue:** If the standard requires underscore-separated endpoint naming (and/or consistent tokenization), this endpoint becomes a one-off exception and sets an unclear precedent for future endpoints.

### A2. Multi-segment, versioned path breaks the otherwise consistent "/beckn/" pattern

- **Where:** `api/beckn.yaml` → `paths./beckn/v2/catalog/publish` and `paths./beckn/v2/catalog/on_publish`
- **Anomaly:** Introduces `v2/catalog` namespacing and versioning inside the endpoint path.
- **Why it's an issue:**
  - Mixed path taxonomy: transaction endpoints are single verb tokens (`/select`, `/init`, etc.) while catalog publish is multi-segment.
  - Unclear whether versioning belongs in the path at all (especially since protocol version also exists in `context.version`).

### A3. Callback naming pattern differs from the standard action/callback pairing used elsewhere

- **Where:** `api/beckn.yaml` → `paths./beckn/v2/catalog/publish` vs `paths./beckn/v2/catalog/on_publish`
- **Anomaly:** Callback endpoint is `on_publish`, but the action endpoint is `publish` nested under `catalog`.
- **Why it's an issue:**
  - Inconsistent depth and naming compared to established pairs like `/select` ↔ `/on_select`, `/init` ↔ `/on_init`.
  - Creates ambiguity about whether the action is `publish`, `catalog_publish`, or `catalog/publish`.

### A4. Compound "context.action" naming diverges from endpoint naming

- **Where:** `api/beckn.yaml` → `/beckn/discover/offer`
  - Request context uses `action: "discover_offer"`
  - Callback uses `action: "on_discover_offer"`
- **Anomaly:** Endpoint is path-tokenized (`/discover/offer`), while `context.action` is underscore-tokenized (`discover_offer`).
- **Why it's an issue:**
  - Unclear canonical representation of action names (path segments vs underscore concatenation).
  - Makes it harder for authors to add new path-parameterized endpoints consistently.

### A5. Legacy action naming exception needs to be explicitly codified

- **Where:** `api/beckn.yaml` → `/beckn/rating` ↔ `/beckn/on_rating`
- **Anomaly:** Uses noun form `rating` rather than expected verb form.
- **Why it's an issue:** Exceptions must be documented to prevent future drift.

---

## B) Schema/Class Naming Anomalies (OpenAPI schemas)

### B1. Folder name includes domain prefix but schema class name does not

- **Where:**
  - `schema/EvChargingService/v1/attributes.yaml` defines `ChargingService`
  - `schema/EvChargingOffer/v1/attributes.yaml` defines `ChargingOffer`
  - `schema/EvChargingSession/v1/attributes.yaml` defines `ChargingSession`
  - `schema/EvChargingPointOperator/v1/attributes.yaml` defines `ChargingPointOperator`
- **Anomaly:** Directory naming suggests an `EvCharging*` prefix is part of the canonical name, but the schema class names omit it.
- **Why it's an issue:**
  - Unclear whether domain specificity should be expressed in the class name, context, folder, or all three.
  - Increases collision risk across future verticals.

### B2. Noun vs Action model ambiguity (schema.org alignment unclear)

- **Where:** `schema/core/v2/attributes.yaml` defines both `Tracking` and `TrackAction`.
- **Anomaly:** Both represent "tracking" concepts, but one is a noun and one is an action.
- **Why it's an issue:** Authors need clear rules for when to use `*Action` schemas vs noun schemas (especially when following schema.org).

---

## C) Property Naming Anomalies (grammar, ambiguity, casing, tautology)

### C1. Use of ambiguous/reserved property name: `type`

- **Where:** `api/beckn.yaml` → `components.schemas.DiscoverRequest.message.filters.type`
- **Anomaly:** Property name `type`.
- **Why it's an issue:** `type` is overloaded in JSON Schema/OpenAPI and is rarely self-describing.

### C2. Inconsistent casing convention: snake_case vs camelCase

- **Where:** `schema/core/v2/attributes.yaml`
  - `AckResponse.transaction_id`, `ack_status`
  - `Tracking.tl_method`, `expires_at`
  - `Form.mime_type`, `submission_id`
- **Anomaly:** snake_case coexists with camelCase properties elsewhere (`paymentURL`, `reservationId`, `lastUpdated`, etc.).
- **Why it's an issue:** Undermines predictable modeling and code generation.

### C3. Abbreviation and unit casing inconsistency

- **Where:**
  - `schema/core/v2/attributes.yaml`: `paymentURL` (URL uppercase)
  - EV charging schemas: `maxPowerKW`, `meteredEnergyKWh`
- **Anomaly:** Casing for abbreviations and unit suffixes isn't standardized.
- **Why it's an issue:** Leads to drift (`Url` vs `URL`, `kWh` vs `KWH`) and hurts readability/searchability.

### C4. Repeated "Attributes" extension points (risk of tautological and unclear semantics)

- **Where:** `schema/core/v2/attributes.yaml`
  - `beckn:itemAttributes`, `beckn:offerAttributes`, `beckn:providerAttributes`, `beckn:orderAttributes`, `beckn:orderItemAttributes`, `beckn:invoiceAttributes`, `beckn:paymentAttributes` — all point to schema `Attributes`.
- **Anomaly:** Heavy reuse of the term "Attributes" at both the property and schema level.
- **Why it's an issue:**
  - Unclear semantics (generic bag vs well-defined extension point).
  - Encourages tautological patterns (e.g., `Billing.billingAttributes` style) in future domains.

### C5. Enum grammar inconsistency: state vs verb

- **Where:** `schema/EvChargingSession/v1/attributes.yaml` → `ChargingSession.sessionStatus` enum includes `STOP` alongside state adjectives (`PENDING`, `ACTIVE`, `COMPLETED`).
- **Why it's an issue:** Inconsistent grammatical form within the same enum.

---

## D) Example Payload and Documentation Mismatches

### D1. Example value casing does not match enum casing

- **Where:** `schema/core/v2/attributes.yaml` → `Tracking.trackingStatus`
  - enum: `[ACTIVE, DISABLED, COMPLETED]`
  - example uses `"active"`
- **Why it's an issue:** Examples become misleading.

### D2. Example values do not match enum values

- **Where:** `schema/core/v2/attributes.yaml` → `SupportInfo.channels`
  - enum: `["PHONE","EMAIL","WEB","CHAT","WHATSAPP","IN_APP","OTHER"]`
  - example uses lowercase values (`"web"`, `"phone"`, `"email"`).
- **Why it's an issue:** Examples contradict schema definitions.

### D3. README refers to a schema/class name that does not exist

- **Where:** `schema/EvChargingService/v1/README.md`
  - References `ChargingProvider` in the attachment table.
  - Actual schema in `schema/EvChargingPointOperator/v1/attributes.yaml` is `ChargingPointOperator`.
- **Why it's an issue:** Spec authors and implementers can't reliably map docs to schemas.

---

## E) Spec-Authoring Structural Issues That Also Create Naming Artifacts

### E1. Invalid schema structure leads to accidental property exposure (`items`)

- **Where:** `schema/EvChargingService/v1/attributes.yaml`
  - `amenityFeature` is declared as `type: array`, but `items:` is not nested under it (indentation bug). As written, `items` becomes a sibling property.
- **Why it's an issue:** This becomes an "absurdity" at the schema level and can unintentionally introduce a property literally named `items`.

---

## F) Cross-Artifact Naming Drift (OpenAPI ↔ JSON-LD ↔ profile.json ↔ README)

### F1. OpenAPI class name vs JSON-LD label diverge

- **Where:**
  - `schema/EvChargingOffer/v1/attributes.yaml`: class is `ChargingOffer`
  - `schema/EvChargingOffer/v1/vocab.jsonld`: label is `"EV Charging Offer"`
- **Why it's an issue:** Inconsistent domain prefix representation. It's unclear what is canonical: folder name, schema name, or label.

### F2. JSON-LD declares a Class that is not a first-class OpenAPI schema

- **Where:** `schema/EvChargingService/v1/vocab.jsonld` defines `ChargingStation` as an `rdfs:Class`.
- **But:** In `schema/EvChargingService/v1/attributes.yaml`, `chargingStation` is an inline object schema.
- **Why it's an issue:** Style guide should clarify when nested objects should be promoted to named reusable schemas/classes.

### F3. Enum tokenization mismatch across artifacts

- **Where:** `schema/EvChargingOffer/v1/vocab.jsonld` includes `schema:alternateName` like `"TIME-OF-DAY"` while YAML enum uses `TIME_OF_DAY`.
- **Why it's an issue:** Underscores vs hyphens are used inconsistently across the stack.

### F4. profile.json uses snake_case naming distinct from schema property naming

- **Where:** `schema/EvChargingService/v1/profile.json` includes keys like:
  - `operational_hints`, `max_offers_per_item`, `item_attributes`, `offer_attributes`, `supported_filters`, `text_search`, `default_sort`
- **Why it's an issue:** Without explicit guidance, different artifacts will adopt different naming conventions and authors won't know what to follow.

---

## G) Editorial/Grammar Issues (Style Guide Scope)

### G1. Typos and duplicated words in schema descriptions

- **Where:** `schema/core/v2/attributes.yaml` → `Form.url.description`
  - Contains `"choosed"` and `"the the"`.
- **Why it's an issue:** The spec should set a baseline for grammatical and semantic correctness in descriptions, not just field names.

---

## Why This Matters

Without an explicit, enforced style guide:

- New domains will introduce conflicting/unclear class names
- Endpoint naming will continue to drift (especially for meta endpoints and multi-segment paths)
- Property naming will remain inconsistent (casing, reserved words, acronyms)
- Docs/examples will keep diverging from schemas
- Cross-artifact inconsistencies will make schema publication + tooling difficult

---

## Proposed Next Steps

*(Follow-up work; not part of this issue)*

1. Create a **Beckn Protocol 2.0 spec-authoring style guide** aligned with schema.org's style guidance.
2. Define a **conformance checklist** for spec PRs:
   - Endpoint tokenization rules
   - Action/callback pairing rules
   - Forbidden/ambiguous property names (e.g., `type`)
   - Casing rules (camelCase vs snake_case) per artifact type
   - Enum vs example consistency
   - Lint checks for common structural errors in YAML

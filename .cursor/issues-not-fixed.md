# Spec Review Notes & Open Questions

## Section 1: By Design (No Change Needed)

These are intentional design decisions with solid reasoning.

| Issue | Location | Reason |
|-------|----------|--------|
| **F1** - JSON-LD label differs from class name | `vocab.jsonld` | **Partially fixed:** Class names now match folder names (e.g., `EvChargingOffer`). The `rdfs:label` ("EV Charging Offer") differs from `@id` (`EvChargingOffer`) - this is standard JSON-LD practice where labels are human-readable. |
| **C4** - Repeated "Attributes" extension points | `core/v2` | Scoped names (`itemAttributes`, `orderAttributes`) are self-documenting. A generic name would lose clarity. |
| **Enum Exception** - `connectorType` casing | `EvChargingService` | Values like `CCS2`, `Type2`, `CHAdeMO`, `GB_T` are industry standard identifiers - kept as-is. |

---

## Section 2: Requires Discussion

These are subjective and need team consensus before implementation.

---

### A5 - `rating` Uses Noun Instead of Verb

**Issue:** `/beckn/rating` uses noun form while other endpoints use verbs (`/select`, `/init`, `/confirm`).

**Discussion needed:**
- Should we rename to `/beckn/rate` for consistency?
- This would be a breaking change for existing implementations.
- Alternative: Document as a legacy exception in the Style Guide.

---

### B2 - Both `Tracking` and `TrackAction` Exist

**Issue:** Two schemas represent "tracking" concepts - one noun, one action.

**Discussion needed:**
- Should we merge them or keep them separate?
- Current rationale: Different purposes
  - `TrackAction` = Simple clickable link (schema.org pattern)
  - `Tracking` = Complex transport/status with method, expiry, etc. (Beckn-specific)
- Need to clarify when to use which in the Style Guide.

---

### C2 - Context Object snake_case

**Issue:** Context properties (`message_id`, `bap_id`, `bap_uri`, etc.) use snake_case while rest of spec uses camelCase.

**Discussion needed:**
- Should we change Context properties to camelCase?
- These have been snake_case since Beckn 1.x inception
- Inherited from external transaction spec

| Option | Pros | Cons |
|--------|------|------|
| **Keep snake_case** | Backward compatible; aligns with Beckn 1.x | Inconsistent with rest of spec |
| **Change to camelCase** | Full consistency | Breaking change; requires coordination with transaction spec |

**Suggestion:** If this is a major version release (2.0), this would be the time to make such a breaking change.

---

### F3 - `alternateName` in vocab.jsonld

**Issue:** Do we need `alternateName` at all in vocab.jsonld?

**Discussion needed:**
- What is the purpose of `alternateName` in our JSON-LD vocabulary?
- Is it for external system interoperability? Human readability? Search/discovery?
- If no clear use case, consider removing them entirely.


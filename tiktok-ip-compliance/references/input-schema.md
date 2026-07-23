# Batch input schema

Use the product link and target market as the minimum fields. Ask only for missing fields that affect a triggered risk topic; do not block a batch for optional fields.

| Field | Priority | Purpose |
|---|---:|---|
| Product link / SKU | Required | Preserve source and identify the row. |
| Target market | Required | Do not reuse rules across markets. |
| Product type / category | High | Route prohibited and qualification checks. |
| Brand / manufacturer | High | Route IP and recall checks. |
| Model, UPC/EAN, batch/lot | High when known | Identify recalls and exact product variants. |
| Claim text | High for cosmetics, health, supplement, child, or medical-like items | Route claim and regulatory checks. |
| Ingredient/material | Conditional | Needed for cosmetics, chemicals, food, and supplements. |
| Battery, liquid, aerosol, magnet | Conditional | Route dangerous-goods/logistics checks. |
| Authorization/certification link | Conditional | Verify brand/category approval where required. |

Normalize equivalent headers before grouping. If a field is absent, mark the corresponding evidence as unknown and use Medium when that unknown may affect eligibility.

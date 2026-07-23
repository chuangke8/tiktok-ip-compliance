---
name: tiktok-ip-compliance
description: Assess product links or spreadsheets for TikTok Shop listing risk, including prohibited goods, intellectual-property infringement, recalls, safety, restricted or invite-only eligibility, dangerous-goods logistics, and local documentation. Use when a user asks to check whether products can be sold on TikTok Shop in one or more countries, asks for TikTok infringement or prohibited-product screening, supplies SKU links or an Excel sheet, or needs a country-specific Excel risk report.
---

# TikTok侵权检测

Perform an evidence-based pre-listing screen; do not represent it as a legal clearance or platform approval. Optimize batches by routing each SKU to the few relevant policy topics instead of rereading all rules.

## Fast batch workflow

1. Normalize the input using `references/input-schema.md`. Preserve original rows. If the target market is missing, offer a numbered market list and wait; do not choose it.
2. Create groups by **market + product type + risk signals** (brand, medical/cosmetic claim, battery/liquid/aerosol, child use, food/supplement, recall identifier). Reuse one policy result only inside the same market/topic group.
3. Read `references/rule-routing-matrix.csv` and select only matching official policy routes. Treat the matrix as routing metadata, never as the current policy text.
4. Check each selected route's `last_verified` value. If older than three calendar days, refresh that market-topic group once from the official TikTok Shop Policy Center / Academy, record the new date and source URL, then apply the refreshed rule to all matching rows.
5. Run fast triage before deep research:
   - **Stop as High:** explicit prohibited item, confirmed recall, credible counterfeit/IP infringement, or a mandatory approval known to be absent.
   - **Continue as Medium:** missing brand/ingredient/batch/certification/authorization, regulated claim, or potential restricted category. Record the missing evidence.
   - **Continue as Low:** no adverse signal in the applicable current policy check. This is not a clearance.
6. Deep-check only rows/groups that trigger a route: prohibited/unsupported/restricted/invite-only eligibility, IP and brand authorization, recall/safety, dangerous goods/logistics, and local documents. Parallelize independent group checks when tools permit; do not duplicate work for identical groups.
7. Generate one `.xlsx` report after all rows are assessed. Use the `spreadsheets` skill and render-inspect every worksheet. Keep original rows and append the required fields below.

## Required workbook columns

Include at least: Product link; Target country/TikTok Shop market; Overall risk; Prohibited-sale risk; Intellectual-property risk; Recall/product-safety risk; Restricted/invite-only/approval risk; Dangerous-goods/logistics risk; Specific reason and official policy basis; Required documents or approval action; Recommended next action; Rule-check date; Official policy source URL.

## Guardrails

- Treat `prohibited`, `unsupported`, `restricted`, and `invite-only` as distinct states.
- Screen IP across the product, packaging, brand name, title, images, description, video/LIVE, shop name, and avatar. An official storefront does not prove another seller has resale authorization.
- Do not downgrade recall risk without product identity, manufacturer, batch/lot, and an appropriate recall-source check.
- Do not broaden cosmetic claims into whitening, medical treatment, cure, prevention, or drug-like claims unless supported and permitted.
- Do not infer product facts from a blocked page, CAPTCHA, or marketplace search snippet; report the evidence gap instead.
- Never reuse a policy result across markets or after its three-calendar-day freshness window.

## References

- Read `references/input-schema.md` when the supplied links or spreadsheet lack product facts.
- Read `references/rule-routing-matrix.csv` to select the smallest relevant set of official policy pages.
- Read `references/official-policy-baseline.md` only when a selected matrix route requires its official URL or regional routing context.

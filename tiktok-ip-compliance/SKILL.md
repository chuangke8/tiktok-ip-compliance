---
name: tiktok-ip-compliance
description: Assess product links or spreadsheets for TikTok Shop listing risk, including prohibited goods, intellectual-property infringement, recalls, safety, restricted or invite-only eligibility, dangerous-goods logistics, and local documentation. Use when a user asks to check whether products can be sold on TikTok Shop in one or more countries, asks for TikTok infringement or prohibited-product screening, supplies SKU links or an Excel sheet, or needs a country-specific Excel risk report.
---

# TikTok侵权检测

Perform an evidence-based pre-listing screen; do not represent it as a legal clearance or a platform approval.

## Workflow

1. Identify each supplied product and its target TikTok Shop market. If the user has not selected a market, offer a numbered market list and wait; do not choose on their behalf.
2. Read `references/official-policy-baseline.md`. Check the snapshot date. If it is more than three calendar days old, refresh the relevant region from the official TikTok Shop Policy Center / Academy before assessing the SKU.
3. Review product facts and official rules for: prohibited goods, unsupported goods, restricted/invite-only approval, IP/brand authorization, recalls and safety, dangerous goods/logistics, and local product/label/document requirements.
4. Separate verified facts from unknowns. A missing brand owner, ingredient, certification, batch, or authorization is a risk signal, not proof of a violation. Do not infer product facts from a blocked page, CAPTCHA, or marketplace search snippet.
5. Assign Low / Medium / High for every risk dimension using the definitions below. Cite the applicable official source URLs and rule-check date.
6. Deliver an `.xlsx` report. For spreadsheet input, preserve every original row and append the assessment columns. Use the `spreadsheets` skill, including its render-and-inspect requirement, to produce the workbook.

## Risk ratings

- **High:** explicit platform prohibition; recall/unsafe signal; credible counterfeit or IP-infringement signal; or a mandatory authorization/document is absent and prevents sale.
- **Medium:** incomplete product evidence; potentially restricted category; uncertain brand authorization; regulated/cosmetic/medical-like claim; or a document needs verification.
- **Low:** no adverse signal found in the current official check. This is not a compliance guarantee.

## Required workbook columns

Include at least: Product link; Target country/TikTok Shop market; Overall risk; Prohibited-sale risk; Intellectual-property risk; Recall/product-safety risk; Restricted/invite-only/approval risk; Dangerous-goods/logistics risk; Specific reason and official policy basis; Required documents or approval action; Recommended next action; Rule-check date; Official policy source URL.

## Guardrails

- Treat `prohibited`, `unsupported`, `restricted`, and `invite-only` as distinct states.
- Screen IP across the product, packaging, brand name, title, images, description, video/LIVE, shop name, and avatar. An official storefront does not prove another seller has resale authorization.
- Do not downgrade recall risk without product identity, manufacturer, batch/lot, and an appropriate recall-source check.
- Do not broaden cosmetic claims into whitening, medical treatment, cure, prevention, or drug-like claims unless supported and permitted.
- Do not bypass a CAPTCHA or login wall. Report the evidence gap and request the needed product details.

## Policy source

Use `references/official-policy-baseline.md` only as a routing aid. Official regional pages and current local law control whenever they differ.

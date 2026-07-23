---
name: tiktok-ip-compliance
description: Assess product links or spreadsheets for TikTok Shop listing risk, including prohibited goods, intellectual-property infringement, recalls, safety, restricted or invite-only eligibility, dangerous-goods logistics, and local documentation. Also compile a daily TikTok update digest from official platform rules and TikTok news when a user says 今日TK更新. Use when a user asks to check whether products can be sold on TikTok Shop in one or more countries, asks for TikTok infringement or prohibited-product screening, supplies SKU links or an Excel sheet, or needs a country-specific Excel risk report.
---

# TikTok侵权检测

Perform an evidence-based pre-listing screen; do not represent it as a legal clearance or platform approval. Optimize batches by routing each SKU to the few relevant policy topics instead of rereading all rules.

## 今日TK更新

Trigger this mode when the user says `今日TK更新`, optionally followed by country/market names (for example, `今日TK更新 美国、印尼`) or `全部`.

1. Use Asia/Shanghai as the reporting date and define the window as local 00:00 through the current time. State the exact window in the result.
2. Read `references/today-update-sources.md`. With no market argument, check global official TikTok news and global official platform-policy announcements only. With market names, add only those markets' TikTok Shop policy sources. Treat `全部` as a wider, slower configured-market scan and list the markets actually covered.
3. Fetch source indexes first. Compare title, published/effective date, version, and content hash with the prior local run state at `%USERPROFILE%\\.codex\\state\\tiktok-ip-compliance\\today-tk-update.json`. Fetch full pages only for new or changed candidates.
4. Classify every item as **confirmed policy change**, **official platform announcement**, **reputable-media report**, or **unverified/insufficient evidence**. Only an official policy source may establish a rule change. Never infer a rule effective date from an article's publishing date.
5. Return a concise Chinese digest: summary counts; rule changes and seller impact/action; TikTok news; no-change/coverage gaps; and source links with observed time. If this is the first run, say that the baseline was created rather than calling prior unseen content a new change.
6. Save the minimal comparison state after a successful run. Do not create a scheduled task, do not write the state into the Skill/repository, and do not bypass CAPTCHA or login walls.

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
- Read `references/today-update-sources.md` only for the `今日TK更新` command.

# 今日TK更新：来源与判定

## 命令和范围

- `今日TK更新`：全球 TikTok 官方新闻与全球官方平台公告；不把未指定国家的消息写成某个 TikTok Shop 市场规则。
- `今日TK更新 美国、印尼`：上述全球范围，加上指定市场的 Seller Policy Center / Academy / Shop 公告。
- `今日TK更新 全部`：检查可定位到官方来源的已配置市场；在结果中逐一列出实际覆盖市场与无法访问的市场。

## 来源优先级

1. **规则依据**：所选市场的 TikTok Shop Seller Policy Center、Academy、Qualification Center、IP Protection Center 与正式公告。规则结论只能来自这里。
2. **官方新闻**：TikTok Newsroom（https://newsroom.tiktok.com/）及 TikTok / TikTok Shop 官方公告。
3. **媒体新闻**：仅使用具署名、发布日期和原始链接的可信媒体报道；标记为“媒体报道”，不能作为规则变更依据。

美国的路由链接见 `rule-routing-matrix.csv` 与 `official-policy-baseline.md`。其他市场从该市场的官方 seller 域名 Policy Center / Academy 首页进入；禁止使用另一市场的政策替代。

## 变化判定和状态

在 `%USERPROFILE%\\.codex\\state\\tiktok-ip-compliance\\today-tk-update.json` 保存每个来源的 URL、标题、来源类别、页面发布日期、规则生效日、版本/内容哈希和最后观察时间。

- 首次运行：建立基线；仅报告在本地当天窗口内有明确日期的内容，不能把旧页面称为“今日新增”。
- 后续运行：标题、版本、发布日期、规则生效日或内容哈希变化才是候选更新；读取原文确认后再列入结果。
- 无法取得明确日期、版本或正文：列入“待验证/覆盖缺口”，不编造变更。

## 结果格式

按以下顺序用中文输出：

1. 报告日期、时间窗口、覆盖市场与来源数量。
2. 已确认规则变更：市场、规则、发布日期/生效日、卖家影响、建议动作、官方链接。
3. 官方平台新闻与媒体新闻：分别标注来源类别和链接。
4. 无确认变更、待验证项与未覆盖来源。

优先输出 10 条以内最重要项目；有明确禁售、资质或 IP 影响的规则变更优先。

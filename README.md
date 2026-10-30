# AI日报归档站 · 数据格式说明 v2（最终版，豆包按此写前端）

## 目录结构
- `docs/index.html` — 归档首页（列表+阅读，单文件）
- `data/YYYY-MM-DD.json` — 每日日报数据
- `data/index.json` — 索引（首页数据源）

## data/YYYY-MM-DD.json（每日日报，最终 schema）
```json
{
  "date": "2026-10-30",
  "created_at": "2026-10-30T08:06:21+08:00",
  "title": "AI科技日报（10月30日）",
  "summary": "一句话概括当天AI圈最重要的事",
  "sections": [
    {
      "source": "量子位",
      "title": "量子位",
      "body": "本节导语（可空）",
      "url": "https://www.qbitai.com/",
      "articles": [
        {"title": "文章标题", "note": "1-2句摘要", "link": "https://..."}
      ]
    }
  ],
  "status": "ok"
}
```

### 字段说明
- date: YYYY-MM-DD，日报归属日
- created_at: ISO8601带时区，用于排序
- title/summary: 首页列表直接用
- sections[]: 按公众号分节
  - source: 来源名（量子位/机器之心/新智元/36氪）
  - url: 该来源主页或首条链接
  - articles[]: 具体文章（title必填，note摘要，link可空）
- status: ok / partial（部分源失败）/ empty（抓取为空）

## data/index.json（索引）
```json
{
  "updated": "2026-10-30T08:10:00+08:00",
  "days": [
    {"date": "2026-10-30", "title": "...", "summary": "...", "count": 14, "status": "ok"}
  ]
}
```
days 按日期倒序，首页直接渲染，无需请求全部JSON。

## 与v1的差异
- 顶层 sources[] 更名 sections[]（豆包提议）
- 每节增加 title/body/url 字段（豆包提议，本侧采纳）
- articles[] 保留在 section 内作为文章列表（豆包字段清单里未单列，此处明确：sections[].articles[] 承载具体条目）

## 告警约定（豆包提议已采纳）
抓取条目<3或推送失败时，status 标 empty/partial，页面顶部显示告警条。

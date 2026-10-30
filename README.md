# AI日报归档站 · 数据格式说明

## 目录结构
- `docs/index.html` — 归档首页（列表+阅读）
- `data/YYYY-MM-DD.json` — 每日日报数据
- `data/index.json` — 全部日报的索引（首页数据源）

## data/YYYY-MM-DD.json 字段定义
```json
{
  "date": "2026-10-30",
  "generated_at": "2026-10-30T08:06:21+08:00",
  "title": "AI科技日报（10月30日）",
  "summary": "一句话概括当天AI圈最重要的事",
  "sources": [
    {
      "name": "量子位",
      "url": "https://www.qbitai.com/",
      "articles": [
        {"title": "文章标题", "note": "1-2句摘要", "link": "https://..."}
      ]
    }
  ],
  "status": "ok"
}
```
status 取值：ok / partial（部分源失败）/ empty（抓取为空）

## data/index.json 字段定义
```json
{
  "updated": "2026-10-30T08:10:00+08:00",
  "days": [
    {"date": "2026-10-30", "title": "AI科技日报（10月30日）", "summary": "...", "count": 14, "status": "ok"}
  ]
}
```
days 按日期倒序，首页直接渲染。

---
name: webthings
description: "This skill should be used when the user asks to \"manage items\", \"add an item\", \"list items\", \"check spending stats\", \"view purchase history\", \"record a purchase\", \"查看物品\", \"添加物品\", \"记录消费\", \"查看统计\", \"花了多少钱\", or mentions webthings/物品管理."
version: 0.1.0
---

# WebThings CLI — 物品管理命令行工具

WebThings is a personal purchase tracking application. Use the `wt` CLI to manage items, categories, and view spending statistics.

## Prerequisites

- WebThings server running at `http://localhost:3001` (or set `WT_API_URL`)
- `wt` command available globally (installed via `npm link` in the webthings project)

## Commands

### List Items

```bash
wt list [--search 关键词] [--category 分类ID] [--page N] [--limit N] [--json]
```

List all items with optional search and filtering. Use `--json` for raw JSON output.

### Show Item Details

```bash
wt show <id> [--json]
```

View full details of a specific item including images and notes.

### Add Item Manually

```bash
wt add --name "物品名称" [--price 价格] [--category 分类ID] [--date YYYY-MM-DD] [--platform 平台] [--notes 备注]
```

Add a single item with explicit fields. Use `wt categories` to find category IDs.

### AI Smart Add

```bash
wt ai "自然语言描述"
```

Parse natural language to create one or more items automatically. Supports multiple items in a single input.

Examples:
```bash
wt ai "昨天买了一杯咖啡花了25元"
wt ai "前天买了一个鼠标170元，3月10日买了一袋热干面5元"
wt ai "上周在京东买了蓝牙耳机299元"
```

### Delete Item

```bash
wt delete <id>
```

Permanently delete an item by its ID.

### Categories

```bash
wt categories [--json]
```

List all available categories with IDs. Use category IDs when adding items manually.

### Statistics

```bash
wt stats [overview|trend|category|platform|price]
```

View spending statistics:
- `overview` (default) — Total items, total value, daily average, max single purchase
- `trend` — Monthly spending trend
- `category` — Breakdown by category
- `platform` — Breakdown by purchase platform
- `price` — Price distribution ranges

### Health Check

```bash
wt health
```

Verify the API server is running and responding.

## Environment Variables

| Variable | Default | Description |
|----------|---------|-------------|
| `WT_API_URL` | `http://localhost:3001/api` | API base URL |

## Common Workflows

**Record a quick purchase**: `wt ai "买了一杯咖啡15元"`

**Check what was bought recently**: `wt list`

**Find items in a category**: `wt list --category 3`

**See total spending**: `wt stats`

**Get detailed JSON for processing**: `wt list --json`

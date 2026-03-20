# SITE.md Template

SITE.md là index file — "bản đồ" để AI và người đọc biết tìm thông tin gì ở đâu. Đây là file đầu tiên AI nên đọc khi bắt đầu làm việc với codebase.

---

## Template

```markdown
# {Project Name} — Documentation Index

{1-2 câu mô tả project: đây là gì, tech stack chính}

## Quick Reference

| Cần tìm | Đọc doc |
|---------|---------|
| Tổng quan kiến trúc | [00-architecture](00-architecture.md) |
| {Main flow} | [01-{flow}](01-{flow}.md) |
| {Core component 1} | [02-{component}](02-{component}.md) |
| {Core component 2} | [03-{component}](03-{component}.md) |
| {External services} | [04-{services}](04-{services}.md) |
| {Data layer} | [05-{data}](05-{data}.md) |
| Deployment & CI/CD | [08-deployment](08-deployment.md) |

## Doc Map

| # | Doc | Responsibility | Depends On |
|---|-----|----------------|------------|
| 00 | [architecture](00-architecture.md) | System shape, component connections | — |
| 01 | [{flow}](01-{flow}.md) | {1-line description} | 00 |
| 02 | [{component}](02-{component}.md) | {1-line description} | 00, 01 |
| 03 | [{component}](03-{component}.md) | {1-line description} | 00, 01 |
| 04 | [{services}](04-{services}.md) | {1-line description} | 02 |
| 05 | [{data}](05-{data}.md) | {1-line description} | 00 |
| 06 | [{storage}](06-{storage}.md) | {1-line description} | 02 |
| 07 | [{frontend}](07-{frontend}.md) | {1-line description} | 05 |
| 08 | [deployment](08-deployment.md) | CI/CD, environments | All |

## Tech Stack

| Layer | Technology |
|-------|-----------|
| {Layer 1} | {Tech} |
| {Layer 2} | {Tech} |
| {Layer 3} | {Tech} |

## Start Here

Nếu bạn là AI agent mới đọc codebase này:
1. Đọc [00-architecture](00-architecture.md) để hiểu tổng quan
2. Đọc doc liên quan đến task bạn đang làm (xem Quick Reference)
3. Follow Cross-References trong từng doc để hiểu context

Nếu bạn là developer mới:
1. Start với [00-architecture](00-architecture.md)
2. Follow số thứ tự 01 → 02 → 03...
```

---

## Khi nào update SITE.md

- Thêm doc mới → thêm vào Quick Reference và Doc Map
- Đổi tên doc → update links
- Thay đổi dependency order → update cột "Depends On"

SITE.md phải luôn là **source of truth** cho navigation.

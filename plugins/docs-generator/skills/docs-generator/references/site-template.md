# SITE.md Template

SITE.md is the index file — the "map" so AI and readers know where to find what information. This is the first file AI should read when starting work with a codebase.

---

## Template

```markdown
# {Project Name} — Documentation Index

{1-2 sentence project description: what this is, main tech stack}

## Quick Reference

| Need to find | Read doc |
|-------------|----------|
| Architecture overview | [00-architecture](00-architecture.md) |
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

If you're an AI agent new to this codebase:
1. Read [00-architecture](00-architecture.md) to understand the overview
2. Read the doc related to your task (see Quick Reference)
3. Follow Cross-References in each doc to understand context

If you're a new developer:
1. Start with [00-architecture](00-architecture.md)
2. Follow the number order 01 → 02 → 03...
```

---

## When to update SITE.md

- Add new doc → add to Quick Reference and Doc Map
- Rename doc → update links
- Change dependency order → update "Depends On" column

SITE.md must always be the **source of truth** for navigation.

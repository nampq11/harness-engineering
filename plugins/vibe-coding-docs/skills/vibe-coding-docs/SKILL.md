---
name: vibe-coding-docs
description: "Write, organize, and refactor documentation for vibe coding projects optimized for both humans and AI agents (Cursor, Claude Code, etc.). Use this skill WHENEVER the user wants to: create docs for a new project, refactor old docs, asks \"AI doesn't understand my codebase\", asks about writing context for AI, or mentions \"documentation\", \"context for AI\", \"vibe coding docs\", \"structured docs\", \"docs for Cursor/Claude Code\". Trigger even when the user just says \"help me write docs\", \"AI keeps answering wrong\", or \"need to document codebase\"."
---

# Vibe Coding Docs Skill

This skill helps create structured documentation for vibe coding projects, optimized for both humans and AI agents (Cursor, Claude Code, Windsurf, etc.) to navigate and extract accurate information.

## Core Philosophy

Good AI documentation isn't about writing more — it's about writing with **predictable structure**. LLMs process tokens through attention weights: headings, tables, and code blocks receive higher attention than regular prose. Information buried in long paragraphs is easily missed or incorrectly extracted by AI.

**Domain partitioning formula:**
```
Domain = Responsibility × Change-frequency × Dependency-level
```

- **Responsibility**: Each doc does ONE thing. Test: describe the doc in one sentence without the word "and".
- **Change-frequency**: Things that change together → go in the same doc.
- **Dependency-level**: Number indicates dependency level. Lower number = foundation, higher number = surface.

---

## Workflow

### Step 1: Inventory & Cluster

First, ask the user (or analyze the codebase if available) to get:
- List of all components/modules in the system
- Tech stack being used
- Project scale (number of files, number of modules)

Then cluster by responsibility. Use 4 questions to classify:

| Question | Purpose |
|----------|---------|
| **Change Q**: "If you change X, do you have to change Y?" | X and Y belong in same doc if yes |
| **Break Q**: "If X breaks, what else breaks?" | Determine order (more breakage → lower number) |
| **Explain Q**: "Can you explain this concept in 3 minutes?" | If no → split it |
| **Find Q**: "Where would someone look for this info?" | Doc must match mental model |

### Step 2: Create file structure

Name files following pattern: `NN-domain-name.md`

Example typical structure:
```
docs/
├── 00-architecture-overview.md   # Foundation, everything depends on this
├── 01-[core-flow].md
├── 02-[main-worker].md
├── 03-[interface-layer].md
├── 04-[external-services].md
├── 05-[data-layer].md
├── 06-[storage].md
├── 07-[frontend].md
├── 08-[deployment].md
└── SITE.md                        # Index, lists all docs
```

The numbering reflects dependency: 00 is foundation (depended on by most things), higher numbers are surface.

### Step 3: Write each doc following skeleton

Each doc MUST follow this skeleton (see `references/doc-skeleton.md`):

```markdown
# NN-domain-name

{2-3 sentence overview: what this is, why it exists}

## System Diagram
{Mermaid diagram}

## 1. First Section
{Table for config/data, avoid prose}

## 2. Second Section
{...}

## File Reference
| File | Purpose |
|------|---------|

## Cross-References
| Doc | Relation |
|-----|----------|
```

**Important rules:**
- Config values, parameters, routes → **always use tables**, don't bury in prose
- Keep each doc at **800–1500 tokens** to fit in one RAG chunk
- Always include **Cross-References** so AI can navigate between docs

### Step 4: Create SITE.md (index)

SITE.md is the map so AI knows where to find what. See template at `references/site-template.md`.

### Step 5: Validate

Checklist before finishing:
- [ ] Each doc has 2-3 sentence overview?
- [ ] Each doc has Mermaid diagram?
- [ ] Config/data in tables, not in prose?
- [ ] All have File Reference?
- [ ] All have Cross-References?
- [ ] SITE.md has been updated?
- [ ] Each doc can be described in one sentence without "and"?

---

## Anti-patterns to avoid

| Anti-pattern | Problem | Solution |
|-------------|---------|----------|
| Organize by file type (models.md, controllers.md) | Feature spans multiple file types, must jump around | Organize by domain/responsibility |
| Alphabetical sorting | No learning path | Sort by dependency level |
| One mega-doc (README.md contains everything) | Can't chunk, can't find anything | Split into multiple small docs |
| Too much prose | AI can't extract, wastes tokens | Use tables for structured data |
| No Cross-References | Each doc is an island | Always link to related docs |

---

## When to read reference files

- Need full template for a doc → read `references/doc-skeleton.md`
- Need to create SITE.md index → read `references/site-template.md`
- Need complete doc example → read `references/example-doc.md`
- Need to understand why tables are better than prose (to explain to user) → read `references/why-structure.md`

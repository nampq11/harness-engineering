# Why Structure Matters for AI

This reference explains the technical reasons why structured docs help AI perform better. Use this to explain to users when they ask "why do I have to write it this way?"

---

## 1. Attention Weights Are Uneven

LLMs don't read like humans — top to bottom, line by line. LLMs process all tokens simultaneously through attention mechanism, and **assign different weights** to different parts.

| Element | Attention level |
|---------|----------------|
| `# Headings` | Very high |
| Tables | High |
| Code blocks | High |
| **Bold text** | Medium-high |
| Regular prose | Low |

**Real-world impact:** Config values buried in long paragraphs → AI may miss or extract incorrectly. Same config in table → AI extracts with near 100% accuracy.

---

## 2. Token Efficiency

Same information, different presentation costs different tokens. Token = cost and context window.

**Comparison example:**

❌ Prose (~47 tokens):
> "Queue has max batch size of 1, meaning it processes one message at a time. Timeout is 5 seconds, max 2 retries before entering dead letter queue vilab-ai-dlq."

✅ Table (~28 tokens):
| Config | Value |
|--------|-------|
| Max batch size | 1 |
| Timeout | 5s |
| Max retries | 2 |
| DLQ | vilab-ai-dlq |

Table saves **~40% tokens** and AI extracts more accurately because structure is clear.

---

## 3. Chunking and RAG

When AI tools like Cursor, Claude Code, or RAG systems read docs, they must split (chunk) content to fit into context window.

**Problem with docs too long:**
- 10,000 token doc gets split into multiple chunks
- Context lost at split points
- AI reads middle chunk, missing overview and cross-references

**Solution:**
- Keep each doc at 800–1500 tokens
- Each doc = 1 domain = 1 chunk
- AI reads complete domain, no cutoff

---

## 4. Predictable Structure Helps Navigation

When all docs have same skeleton (Overview → Diagram → Sections → File Ref → Cross-Refs), AI learns the pattern:

- "Need to know related files → find ## File Reference"
- "Need to know config values → find table in numbered sections"
- "Need broader context → follow Cross-References"

Not predictable → AI must "guess" structure per doc → wastes attention, prone to errors.

---

## 5. Cross-References = Navigation Graph

AI agents don't read docs in order. They search and jump by context.

Cross-References create **navigation graph** so AI can:
1. Read doc A, see need for more context
2. Follow Cross-Reference to doc B
3. No need to search from beginning

Missing Cross-References → each doc is an island → AI gets lost when needing cross-domain context.

---

## Summary

| Problem | Solution |
|---------|----------|
| AI misses info in prose | Use tables and headings |
| Doc too long → RAG chunking errors | Keep 800-1500 tokens/doc |
| AI doesn't know where to find what | Consistent skeleton + SITE.md index |
| AI loses context when needing cross-domain | Cross-References at end of each doc |
| Token cost too high | Tables instead of prose for structured data |

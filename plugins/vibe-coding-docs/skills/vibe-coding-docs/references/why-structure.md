# Tại sao Structure quan trọng với AI

Reference này giải thích kỹ thuật đằng sau tại sao structured docs giúp AI hoạt động tốt hơn. Dùng để giải thích cho user khi họ hỏi "tại sao phải viết như vậy?"

---

## 1. Attention Weights không đều

LLM không đọc như người — từ trên xuống, từng dòng. LLM xử lý tất cả tokens cùng lúc thông qua cơ chế attention, và **gán trọng số khác nhau** cho từng phần.

| Element | Mức attention |
|---------|--------------|
| `# Headings` | Rất cao |
| Tables | Cao |
| Code blocks | Cao |
| **Bold text** | Trung bình-cao |
| Văn xuôi thường | Thấp |

**Hệ quả thực tế:** Config values chôn trong paragraph dài → AI có thể bỏ sót hoặc extract sai. Cùng config đó trong table → AI extract chính xác gần như 100%.

---

## 2. Token Efficiency

Cùng thông tin, cách trình bày khác nhau tốn token khác nhau. Token = chi phí và context window.

**Ví dụ so sánh:**

❌ Văn xuôi (~47 tokens):
> "Queue có max batch size là 1, nghĩa là xử lý từng message một. Timeout là 5 giây, retry tối đa 2 lần trước khi vào dead letter queue vilab-ai-dlq."

✅ Table (~28 tokens):
| Config | Value |
|--------|-------|
| Max batch size | 1 |
| Timeout | 5s |
| Max retries | 2 |
| DLQ | vilab-ai-dlq |

Table tiết kiệm **~40% tokens** và AI extract chính xác hơn vì structure rõ ràng.

---

## 3. Chunking và RAG

Khi AI tools như Cursor, Claude Code, hay các RAG systems đọc docs, chúng phải chia nhỏ (chunk) content để fit vào context window.

**Vấn đề với doc quá dài:**
- Doc 10,000 tokens bị cắt thành nhiều chunks
- Context bị mất ở chỗ cắt
- AI đọc chunk giữa chừng, thiếu overview và cross-references

**Giải pháp:**
- Giữ mỗi doc ở 800–1500 tokens
- Mỗi doc = 1 domain = 1 chunk
- AI đọc trọn vẹn 1 domain, không bị cắt ngang

---

## 4. Predictable Structure giúp Navigation

Khi tất cả docs có cùng skeleton (Overview → Diagram → Sections → File Ref → Cross-Refs), AI học được pattern:

- "Cần biết files liên quan → tìm ## File Reference"
- "Cần biết config values → tìm table trong numbered sections"
- "Cần context rộng hơn → follow Cross-References"

Không predictable → AI phải "đoán" structure mỗi doc → tốn attention, dễ sai.

---

## 5. Cross-References = Navigation Graph

AI agents không đọc docs theo thứ tự. Chúng search và jump theo context.

Cross-References tạo ra **navigation graph** để AI có thể:
1. Đọc doc A, thấy cần context thêm
2. Follow Cross-Reference đến doc B
3. Không cần search lại từ đầu

Thiếu Cross-References → mỗi doc là hòn đảo → AI bị lost khi cần cross-domain context.

---

## Tóm tắt

| Vấn đề | Giải pháp |
|--------|----------|
| AI bỏ sót info trong văn xuôi | Dùng tables và headings |
| Doc quá dài → RAG chunking lỗi | Giữ 800-1500 tokens/doc |
| AI không biết tìm gì ở đâu | Skeleton nhất quán + SITE.md index |
| AI mất context khi cần cross-domain | Cross-References ở cuối mỗi doc |
| Token tốn quá nhiều | Table thay vì văn xuôi cho structured data |

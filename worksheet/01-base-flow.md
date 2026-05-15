# 01 · Base Flow + Chốt 3 Knobs

> **Mục tiêu**: Hiểu chatbot hoạt động ra sao ở mức base (không chọn config gì) và xác định 3 knobs nhóm sẽ tweak ở các bước sau.
>
> **Thời gian**: 7 phút (trong 15 phút phần Setup)

---

## Bước 1 — Base flow của nhóm

```text
Tourist message
  -> Intent classification (keyword/LLM)
      -> Guide: RAG top-5 -> Context assembly -> Response
      -> Visa: RAG + Web search -> Context assembly -> Response
      -> Weather: Web search + RAG -> Context assembly -> Response
      -> Booking: Handoff to sales (template reply, no LLM generation)
      -> Complaint: Escalate to manager (template reply, no LLM generation)

Context assembly = system prompt + selected history + RAG/web evidence + current user msg.
```

---

## Bước 2 — Chốt 3 knobs

### Knob 1 — Model tier

```text
Nhóm ưu tiên cost-efficiency nhưng vẫn cần đủ chất lượng cho câu hỏi visa và itinerary.
Hướng đi hợp lý là không dùng một model duy nhất: cheap cho FAQ đơn giản, model mạnh hơn cho intent có rủi ro sai thông tin.
Classifier nên giữ ổn định để tránh route nhầm ngay từ bước đầu.
```

### Knob 2 — Web search

```text
Visa và weather là hai intent bắt buộc phải có dữ liệu mới, nên web search nên bật chọn lọc.
Bật web quá rộng làm tăng API cost theo volume và tăng latency, không cần thiết cho các câu guide tĩnh.
=> Ưu tiên ON selective thay vì ON broad cho config cân bằng.
```

### Knob 3 — History management

```text
Scenario B có 7 turns nên history ảnh hưởng rõ đến cost; full history giúp chất lượng nhưng đội chi phí.
Last 3 rẻ nhất nhưng dễ mất ngữ cảnh ngân sách/sở thích từ đầu hội thoại.
Nhóm chọn Last 5 cho cấu hình cân bằng và Full cho cấu hình premium.
```

---

## Bước 3 — Combo dự kiến

**Combo 1 (cheap):**

```text
Model: Gemini 2.5 Flash-Lite
Web: ON selective (Visa, Weather)
History: Last 3
Tên dự kiến: Budget Bot
```

**Combo 2 (premium):**

```text
Model: Claude Opus 4.7
Web: ON broad
History: Full
Tên dự kiến: Premium Concierge
```

**Combo 3 (balanced):**

```text
Model: Smart Mix theo intent
Web: ON selective
History: Last 5
Tên dự kiến: Smart Mix
```

**Combo 4 (optional):**

```text
Model: Budget mùa thấp / Smart Mix mùa cao
Web: ON selective
History: Last 5
Tên dự kiến: Seasonal Switch
```

---

## Bảng kiểm trước khi sang file tiếp theo

- [x] Đã vẽ flow base có đủ 4 bước (Intent → Route → Context → Response)
- [x] Hiểu Booking + Khiếu nại = $0 LLM cost (chuyển con người)
- [x] Đã phác thảo ≥3 combo khác nhau
- [x] Nhóm đồng thuận về hướng đi mỗi combo

Xong → mở `02-config-design.md`.


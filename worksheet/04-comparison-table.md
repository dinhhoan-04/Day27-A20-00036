# 04 · Comparison Table — Bảng so sánh đầy đủ

> **Mục tiêu**: Tổng hợp tất cả số đã tính ở `03-cost-calculation.md` thành 1 bảng so sánh duy nhất để present.

---

## Bảng chính

| | Config 1 | Config 2 | Config 3 | (Config 4) |
|---|---|---|---|---|
| **Tên** | Budget Bot | Premium Concierge | Smart Mix | Seasonal Switch (optional) |
| **1) Model** | Gemini 2.5 Flash-Lite | Claude Opus 4.7 | Guide: Gemini 2.5 Flash; Visa/Weather: DeepSeek V4 Pro | Budget low season, Smart Mix high season |
| **2) Web search** | ON selective (Visa, Weather) | ON broad | ON selective (Visa, Weather) | ON selective |
| **3) History** | Last 3 | Full | Last 5 | Last 5 |
| **Intent classifier** | Keyword | LLM (GPT-4o-mini) | LLM (GPT-4o-mini) | LLM/Keyword theo mùa |
| **Cost / conv (Scenario A — 4 turns)** | $0.00811 | $0.08376 | $0.01759 | N/A |
| **Cost / conv (Scenario B — 7 turns)** | $0.01009 | $0.10237 | $0.02283 | N/A |
| **Monthly A** (300 conv/day × 30) | $73.00 | $753.88 | $158.31 | N/A |
| **Monthly B** (1,200 conv/day × 30) | $363.11 | $3,685.25 | $821.99 | N/A |
| **vs human $4,500/mo (A)** | rẻ 61.64× | rẻ 5.97× | rẻ 28.43× | N/A |
| **vs human $18,000/mo (B)** | rẻ 49.57× | rẻ 4.88× | rẻ 21.90× | N/A |
| **Savings % (A)** | 98.38% | 83.25% | 96.48% | N/A |
| **Savings % (B)** | 97.98% | 79.53% | 95.43% | N/A |
| **Quality estimate** | Medium-Low | High | Medium-High | Medium-High |
| **Speed estimate** | High | Low | Medium | Medium-High |
| **Điểm yếu chính** | Dễ quên context hội thoại dài | Cost cao, latency cao | Routing phức tạp hơn | Cần playbook chuyển mùa rõ ràng |
| **Best for** | Low season, ngân sách chặt | Dịch vụ cao cấp, câu hỏi khó | Mặc định cả năm | DN có seasonality rõ |

---

## Quan sát nhanh từ bảng

### Câu 1 — Config rẻ nhất và đắt nhất

```text
Rẻ nhất: Budget Bot — monthly B = $363.11
Đắt nhất: Premium Concierge — monthly B = $3,685.25
Chênh: 10.15× lần
```

### Câu 2 — Knob nào ảnh hưởng cost nhiều nhất?

```text
Model tier ảnh hưởng lớn nhất.
Đổi từ Flash-Lite (Budget) sang Opus (Premium) làm monthly B tăng ~10.15×.
History Full và web broad tiếp tục đẩy cost lên, nhưng nhỏ hơn tác động của model tier.
```

### Câu 3 — Tại sao Scenario B không đắt ×4 hoặc ×7?

```text
Scenario B có volume ×4 và turns dài hơn, nhưng intent mix có 45% Booking + Complaint (handoff)
nên không tốn LLM như các intent AI-served.
Vì vậy monthly B tăng mạnh nhưng không tới mức A ×7.
```

### Câu 4 — Có config nào AI đắt hơn human không?

```text
Không có config nào đắt hơn human baseline trong 2 scenarios.
Ngay cả Premium Concierge vẫn rẻ hơn human ~4.88× ở mùa cao điểm.
```

---

## Bảng kiểm trước khi sang file tiếp theo

- [x] Bảng đầy đủ, không còn ô trống quan trọng
- [x] Đã có 4 câu trả lời quan sát
- [x] Nhóm đồng thuận về số trong bảng

Xong → mở `05-recommendation.md`.


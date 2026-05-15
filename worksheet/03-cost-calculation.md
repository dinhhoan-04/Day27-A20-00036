# 03 · Cost Calculation — Tính chi phí từng Config × 2 Scenarios

> **Mục tiêu**: Với mỗi config ở `02-config-design.md`, tính cost/turn → cost/conversation → monthly cho cả 2 scenarios.
>
> **Thời gian**: 55 phút

---

## Setup chung

```text
System prompt:              500 tokens
User message:                80 tokens
Assistant response:         180 tokens (output)
1 prior turn (history):     260 tokens
RAG top-5 chunks:         1,250 tokens
Web search results:         800 tokens (khi bật)
Web search API:            $0.005 / call
LLM classifier:            ~$0.000035 / turn (nếu dùng)
```

**Scenario A (low season)**

```text
Volume: 300 conversations/day
Turns/conv: avg 4
Intent mix: Guide 50%, Visa 25%, Weather 10%, Booking 10%, Complaint 5%
```

**Scenario B (high season)**

```text
Volume: 1,200 conversations/day
Turns/conv: avg 7
Intent mix: Guide 30%, Visa 15%, Weather 10%, Booking 35%, Complaint 10%
```

Human baseline: **$0.50 / conversation**

---

## Ví dụ intent-level cost (Budget Bot)

```text
cost_conv_guide   (4 turns) = $0.001176
cost_conv_visa    (4 turns) = $0.021496
cost_conv_weather (4 turns) = $0.021496
cost_1_turn_only             = $0.000000
```

---

## Config 1 — Budget Bot

| Item | Scenario A (4 turns) | Scenario B (7 turns) |
|---|---|---|
| Cost / conversation (avg) | $0.00811 | $0.01009 |
| Monthly cost | $73.00 | $363.11 |
| Human baseline | $4,500 | $18,000 |
| **Rẻ hơn human** | 61.64× | 49.57× |
| **Savings %** | 98.38% | 97.98% |

**Sanity check**:

```text
Cost/conv nằm trong vùng cheap config có web selective.
Scenario B tăng ~4.97× so với A do volume và số turns cao hơn.
```

---

## Config 2 — Premium Concierge

| Item | Scenario A | Scenario B |
|---|---|---|
| Cost / conversation (avg) | $0.08376 | $0.10237 |
| Monthly cost | $753.88 | $3,685.25 |
| **Rẻ hơn human** | 5.97× | 4.88× |
| **Savings %** | 83.25% | 79.53% |

**Sanity check**:

```text
Đây là config đắt nhất trong 3 config, nhưng vẫn rẻ hơn human baseline.
Monthly B > $3,000 đúng với profile premium.
```

---

## Config 3 — Smart Mix

| Item | Scenario A | Scenario B |
|---|---|---|
| Cost / conversation (avg) | $0.01759 | $0.02283 |
| Monthly cost | $158.31 | $821.99 |
| **Rẻ hơn human** | 28.43× | 21.90× |
| **Savings %** | 96.48% | 95.43% |

**Sanity check**:

```text
Nằm giữa Budget và Premium đúng mục tiêu balanced.
Tăng chất lượng cho visa/weather nhưng cost vẫn thấp hơn Premium nhiều lần.
```

---

## Config 4 (optional)

| Item | Scenario A | Scenario B |
|---|---|---|
| Cost / conversation (avg) | N/A | N/A |
| Monthly cost | N/A | N/A |
| **Rẻ hơn human** | N/A | N/A |
| **Savings %** | N/A | N/A |

---

## Quality + Speed estimate (qualitative)

| Config | Quality | Speed | Lý do |
|---|---|---|---|
| 1: Budget Bot | Medium-Low | High | Cheap model + last3 nhanh, nhưng dễ mất context conversation dài. |
| 2: Premium Concierge | High | Low | Opus + web broad + full history cho quality cao nhất nhưng latency cao. |
| 3: Smart Mix | Medium-High | Medium | Intent quan trọng dùng model mạnh, guide dùng model vừa. |
| 4: Seasonal Switch (optional) | Medium-High | Medium-High | Chuyển profile theo mùa để cân bằng chi phí và quality. |

---

## Bảng kiểm trước khi sang file tiếp theo

- [x] ≥3 configs đã có cost/conv + monthly cho cả 2 scenarios
- [x] Đã so sánh từng config với human baseline
- [x] Có quality + speed estimate cho mỗi config
- [x] Đã sanity check các con số

Xong → mở `04-comparison-table.md`.


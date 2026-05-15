# 02 · Configuration Design — Đặt tên + Chốt knobs cho ≥3 Configs

> **Mục tiêu**: Biến phác thảo ở `01-base-flow.md` thành ≥3 configurations chi tiết, mỗi config có tên + 3 knobs đã chốt + lý do chọn.
>
> **Thời gian**: 15 phút (đầu phần Main, trước khi tính cost)

---

## Config 1

**Tên config**:

```text
Budget Bot
```

### 3 Knobs

**① Model tier**:

```text
Response model: Gemini 2.5 Flash-Lite → giá $0.10 / $0.40 per 1M tokens (input/output)
Classifier model: Keyword routing rule → $0
```

**② Web search**:

```text
□ OFF
☑ ON selective — bật cho intent: Visa/Policy, Weather/Event
□ ON broad
```

**③ History management**:

```text
☑ Last 3
□ Last 5
□ Full
□ Summarize every 5 turns
```

### Lý do nhóm chọn config này

```text
Config này phù hợp low season hoặc khung giờ đêm khi cần giảm chi phí tối đa.
Model rẻ giúp cost/conv rất thấp, nhưng vẫn bật web selective cho visa/weather để tránh thông tin cũ.
Đây là baseline tốt để quản lý ngân sách trước khi scale lên model mạnh hơn.
```

### Rủi ro lớn nhất

```text
Last 3 có thể làm mất context ở conversation dài, dễ trả lời thiếu nhất quán từ turn 6–7.
```

---

## Config 2

**Tên config**:

```text
Premium Concierge
```

### 3 Knobs

**① Model tier**:

```text
Response model: Claude Opus 4.7 → giá $5.00 / $25.00 per 1M tokens
Classifier model: GPT-4o-mini → giá $0.15 / $0.60 per 1M tokens
```

**② Web search**:

```text
□ OFF
□ ON selective — bật cho intent: Visa/Policy, Weather/Event
☑ ON broad
```

**③ History management**:

```text
□ Last 3
□ Last 5
☑ Full
□ Summarize every 5 turns
```

### Lý do nhóm chọn config này

```text
Config này ưu tiên chất lượng cao và tính nhất quán cho khách quốc tế có nhu cầu phức tạp.
Full history + web broad giảm rủi ro thiếu context hoặc dùng thông tin cũ.
Phù hợp khi công ty muốn định vị dịch vụ cao cấp và chấp nhận chi phí cao hơn.
```

### Rủi ro lớn nhất

```text
Cost tăng nhanh theo volume vì vừa dùng premium model vừa bật web rộng.
```

---

## Config 3

**Tên config**:

```text
Smart Mix
```

### 3 Knobs

**① Model tier**:

```text
Response model: Guide = Gemini 2.5 Flash ($0.30/$2.50), Visa+Weather = DeepSeek V4 Pro ($1.74/$3.48)
Classifier model: GPT-4o-mini → giá $0.15 / $0.60 per 1M tokens
```

**② Web search**:

```text
□ OFF
☑ ON selective — bật cho intent: Visa/Policy, Weather/Event
□ ON broad
```

**③ History management**:

```text
□ Last 3
☑ Last 5
□ Full
□ Summarize every 5 turns
```

### Lý do nhóm chọn config này

```text
Config này tối ưu theo intent: guide dùng model tầm trung để tiết kiệm, visa/weather dùng model mạnh để tăng độ chính xác.
Web selective giữ API cost vừa phải nhưng vẫn đảm bảo real-time cho intent nhạy cảm.
Last 5 cân bằng giữa chất lượng conversation dài và ngân sách vận hành.
```

### Rủi ro lớn nhất

```text
Vận hành phức tạp hơn vì cần maintain routing logic theo intent và theo model.
```

---

## Config 4 (optional)

**Tên config**:

```text
Seasonal Switch (optional)
```

### 3 Knobs

```text
Model: Budget Bot ở low season, Smart Mix ở high season
Web: ON selective
History: Last 5
```

### Lý do

```text
Ý tưởng này giảm cost khi nhu cầu thấp và tăng chất lượng khi vào mùa cao điểm.
Nhóm chưa tính số chi tiết cho config 4 trong vòng lab.
```

---

## Bảng kiểm trước khi tính cost

- [x] ≥3 configs đã đặt tên
- [x] Mỗi config đã chốt rõ 3 knobs
- [x] Mỗi config có ≥2 câu lý do
- [x] 3 configs đủ khác biệt
- [x] Nhóm đồng thuận đây là 3 configs đáng so sánh

Xong → mở `03-cost-calculation.md`.


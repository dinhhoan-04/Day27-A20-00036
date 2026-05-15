# 05 · Recommendation + Justification — Kết luận & Chuẩn bị Present

> **Mục tiêu**: Chọn 1 config nhóm recommend deploy, viết justification ngắn gọn, và chuẩn bị 5 phút present.

---

## 4 câu hỏi PM cần trả lời

### Câu 1 — Recommend config nào?

```text
Nhóm recommend deploy Smart Mix làm cấu hình mặc định cho cả 2 scenarios.
Lý do: cost vẫn rất thấp so với human (rẻ hơn 28.43× ở Scenario A và 21.90× ở Scenario B),
nhưng quality tốt hơn Budget Bot cho các intent rủi ro như visa/weather.
Nếu chỉ được chọn 1 config quanh năm, Smart Mix là điểm cân bằng tốt nhất.
```

### Câu 2 — So với human baseline $0.50/conv tiết kiệm bao nhiêu?

```text
Smart Mix tiết kiệm 96.48% ở Scenario A và 95.43% ở Scenario B.
Ước tính tiết kiệm khoảng $4,341.69/tháng (A) và $17,178.01/tháng (B).
Trong mô phỏng này, Smart Mix không có điểm nào đắt hơn human.
```

### Câu 3 — Khi nào nên upgrade / downgrade?

```text
Upgrade lên Premium khi complaint về quality >5% liên tục 2 tuần,
hoặc khi conversion từ khách cao cấp tăng rõ ràng.
Downgrade về Budget khi low season kéo dài và KPI quality vẫn đạt.
Theo dõi 4 chỉ số: volume, complaint rate, conversion rate, SLA response.
```

### Câu 4 — Rủi ro lớn nhất của config được chọn?

```text
Rủi ro lớn nhất của Smart Mix là route sai intent (đặc biệt visa/weather),
làm câu hỏi quan trọng bị đẩy sang model yếu hơn.
Mitigation: theo dõi confusion matrix classifier hằng tuần,
và fallback sang model mạnh khi confidence thấp.
```

---

## Final answer — 1 paragraph

```text
Nhóm recommend Smart Mix là cấu hình deploy mặc định vì đạt cân bằng tốt nhất giữa chi phí và trải nghiệm. Trong mô phỏng, Smart Mix có cost trung bình $0.01759/conv ở Scenario A và $0.02283/conv ở Scenario B, thấp hơn human lần lượt 28.43× và 21.90×. So với Budget Bot, Smart Mix tăng chi phí nhưng cải thiện rõ chất lượng ở intent nhạy cảm như visa/weather. So với Premium Concierge, Smart Mix giữ được phần lớn lợi ích quality nhưng tránh mức cost và latency quá cao. Nhóm đề xuất theo dõi complaint rate, conversion rate và chi phí tháng để quyết định khi nào nâng/hạ cấu hình theo mùa. Với mục tiêu unit economics bền vững, đây là lựa chọn hợp lý nhất.
```

---

## Chuẩn bị Present (5 phút)

### Nhịp 0:00–0:30 — Base flow + 3 knobs

Ai trình bày: Đỗ Đình Hoàn - 2A202600036

```text
Flow nhóm dựa trên 3 knobs: model tier, web search, history.
Nhóm tạo 3 configs để so tradeoff cost-quality-speed thay vì tối ưu một chiều.
```

### Nhịp 0:30–1:00 — Config overview

Ai trình bày: Đỗ Đình Hoàn - 2A202600036

```text
1) Budget Bot: cheap model + web selective + last 3.
2) Premium Concierge: Opus + web broad + full history.
3) Smart Mix: model theo intent + web selective + last 5.
```

### Nhịp 1:00–2:00 — Cost comparison

Ai trình bày: Đỗ Đình Hoàn - 2A202600036

```text
Scenario B: Budget = $363.11/tháng, Smart Mix = $821.99/tháng, Premium = $3,685.25/tháng.
Tất cả đều rẻ hơn human baseline $18,000/tháng.
Smart Mix là điểm cân bằng: chi phí thấp hơn Premium nhiều lần nhưng quality cao hơn Budget.
```

### Nhịp 2:00–3:00 — Key insight

Ai trình bày: Đỗ Đình Hoàn - 2A202600036

```text
Knob tác động mạnh nhất là model tier: đổi từ Flash-Lite sang Opus làm monthly B tăng khoảng 10.15×.
Web broad và full history tiếp tục đẩy cost tăng, đặc biệt ở conversation dài.
```

### Nhịp 3:00–4:30 — Recommendation + justification

Ai trình bày: Đỗ Đình Hoàn - 2A202600036

```text
Nhóm recommend Smart Mix là cấu hình deploy mặc định vì đạt cân bằng tốt nhất giữa chi phí và trải nghiệm. Trong mô phỏng, Smart Mix có cost trung bình $0.01759/conv ở Scenario A và $0.02283/conv ở Scenario B, thấp hơn human lần lượt 28.43× và 21.90×. So với Budget Bot, Smart Mix tăng chi phí nhưng cải thiện rõ chất lượng ở intent nhạy cảm như visa/weather. So với Premium Concierge, Smart Mix giữ được phần lớn lợi ích quality nhưng tránh mức cost và latency quá cao. Nhóm đề xuất theo dõi complaint rate, conversion rate và chi phí tháng để quyết định khi nào nâng/hạ cấu hình theo mùa. Với mục tiêu unit economics bền vững, đây là lựa chọn hợp lý nhất.
```

### Nhịp 4:30–5:00 — Hardest question prep

Ai trình bày: Đỗ Đình Hoàn - 2A202600036

```text
Nếu provider tăng giá API ×2 và vẫn giữ SLA hiện tại, config nào còn hợp lý nhất?
```

Câu trả lời sẵn:

```text
Smart Mix vẫn có biên an toàn vì hiện tại rẻ hơn human rất xa.
Bước ứng phó đầu tiên: giảm web broad, giữ web selective, tối ưu routing/fallback trước khi giảm chất lượng model.
```

---

## Q&A quick prep

```text
1. Model tier ảnh hưởng cost nhiều nhất vì giá token model mạnh cao hơn cheap model nhiều lần.
2. Nếu giá API ×2, Smart Mix vẫn sống được; ưu tiên tối ưu routing + web selective trước.
3. Nhóm chọn Smart Mix vì ưu tiên cân bằng dài hạn, không tối thiểu cost như Budget và không tối đa cost như Premium.
```

---

## Bảng kiểm cuối cùng

- [x] Đã trả lời 4 câu PM
- [x] Final answer paragraph rõ ràng, có số cụ thể
- [x] Đã phân công 5 nhịp present
- [x] Đã có câu trả lời cho Q&A khó
- [x] Comparison table sẵn sàng để chiếu


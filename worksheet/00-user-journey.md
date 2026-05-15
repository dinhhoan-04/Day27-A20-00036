# 00 · User Journey Simulation — Đóng vai Tourist

> **Mục tiêu**: Trước khi tính chi phí, nhóm phải hình dung được khách hàng thật sự hỏi gì, hỏi như thế nào, và 1 conversation thực tế trông ra sao.
>
> **Thời gian**: 8 phút (trong 15 phút phần Setup)

---

## Bước 1 — Mỗi người đóng vai 1 tourist (4 phút)

### Tourist #1 (Tên thành viên: Đỗ Đình Hoàn - 2A202600036)

```text
1) Do I need a visa if I hold a US passport and stay in Vietnam for 12 days?
2) Is Hanoi safe for a solo female traveler at night?
3) Which area should I stay in Hanoi for local food and easy walking?
4) What's a good 5-day itinerary for Hanoi and Ha Long Bay?
5) Can I pay by card in most places, or should I carry cash?
6) What is the weather like in late July, and what should I pack?
```

### Tourist #2 (Tên thành viên: Đỗ Đình Hoàn - 2A202600036)

```text
1) We are a family of four with two kids. Which city is easiest for first-time visitors?
2) Can you suggest kid-friendly activities in Da Nang and Hoi An?
3) What is a realistic daily budget for mid-range hotels and food?
4) Are there any big festivals in June that could affect hotel prices?
5) Is travel insurance required for visa on arrival?
6) Can your company arrange a private airport transfer?
```

### Tourist #3 (Tên thành viên: Đỗ Đình Hoàn - 2A202600036)

```text
1) I only have 3 days in Vietnam. Should I choose Hanoi or Ho Chi Minh City?
2) What are the best local foods to try in Ho Chi Minh City for first-timers?
3) Is tap water safe to drink, or should I buy bottled water?
4) Which eSIM option gives the best coverage across Vietnam?
5) I want a private Mekong Delta day tour for 2 people. How much does it cost?
6) My driver was 40 minutes late yesterday. How can I file a complaint?
```

---

## Bước 2 — Gom lại và phân loại (4 phút)

| # | Câu hỏi (1 dòng) | Intent thuộc loại nào | Cần bao nhiêu lượt chat để xong? | Bot trả lời hay chuyển người? |
|---|---|---|---|---|
| 1 | US passport cần visa cho 12 ngày không? | Visa/Policy | 4 lượt | ☑ Bot · □ Người |
| 2 | Thời tiết Hà Nội cuối tháng 7 ra sao? | Thời tiết/Sự kiện | 3 lượt | ☑ Bot · □ Người |
| 3 | Lịch trình 5 ngày Hà Nội + Hạ Long | Điểm đến/Guide | 5 lượt | ☑ Bot · □ Người |
| 4 | Hoạt động phù hợp cho trẻ em ở Đà Nẵng/Hội An | Điểm đến/Guide | 4 lượt | ☑ Bot · □ Người |
| 5 | Budget/ngày cho khách tầm trung | Điểm đến/Guide | 3 lượt | ☑ Bot · □ Người |
| 6 | Lễ hội tháng 6 có làm tăng giá khách sạn không? | Thời tiết/Sự kiện | 3 lượt | ☑ Bot · □ Người |
| 7 | Đặt private airport transfer | Tour/Booking | 1 lượt | □ Bot · ☑ Người |
| 8 | Báo giá + đặt private Mekong Delta tour | Tour/Booking | 1 lượt | □ Bot · ☑ Người |
| 9 | Khiếu nại tài xế đón trễ 40 phút | Khiếu nại | 1 lượt | □ Bot · ☑ Người |
| 10 | Hà Nội có an toàn cho nữ đi một mình buổi tối không? | Điểm đến/Guide | 3 lượt | ☑ Bot · □ Người |

---

## Bước 3 — Rút insight cho nhóm

**Tổng số câu hỏi nhóm gom được**:

```text
18 câu hỏi (3 thành viên × 6 câu mỗi người)
```

**Phân bố intent thực tế của nhóm** (% mỗi intent):

```text
Guide: 40%
Visa: 10%
Weather: 20%
Booking: 20%
Khiếu nại: 10%
```

**Số lượt chat trung bình để xong 1 chủ đề**:

```text
Thông tin (Guide/Visa/Weather): trung bình 3–4 lượt.
Booking/Khiếu nại: 1 lượt để chuyển người.
```

**Đối chiếu với đề bài** (Scenario A = 4 lượt, Scenario B = 7 lượt):

```text
Khá hợp lý với đề bài: Scenario A = 4 lượt gần sát thực tế nhóm quan sát.
Khác biệt chính là booking + khiếu nại trong dữ liệu nhóm cao hơn đề bài, nên AI-served ratio của nhóm thấp hơn một chút.
```

**Insight bất ngờ — điều gì nhóm chỉ hiểu sau khi đóng vai?**

```text
Tourist thường chuyển intent rất nhanh trong cùng một conversation (ví dụ hỏi itinerary rồi nhảy sang visa).
Câu hỏi booking/khiếu nại ngắn nhưng đòi hỏi handoff chuẩn; nếu bot xử lý sai routing sẽ ảnh hưởng trải nghiệm ngay.
```

---

## Bảng kiểm trước khi sang file tiếp theo

- [x] Mỗi người trong nhóm đã viết ≥5 câu hỏi tourist
- [x] Đã gom + phân loại intent cho ≥10 câu (bảng trên)
- [x] Đã có phân bố intent % của nhóm (so với đề bài)
- [x] Có ít nhất 1 insight về cách tourist thật sự dùng chatbot

Xong → mở `01-base-flow.md`.


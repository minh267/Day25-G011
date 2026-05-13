---
artifact: 1 — Demo giao diện
format: ASCII UI sketch
---

# demo.md — Demo giao diện

Demo minh họa cách giao diện giảm rủi ro T-01: AI không được biến thành người quyết định vay nợ/cắt khoản thiết yếu thay user.

---

## 1. Màn hình chính

```text
┌──────────────────────────────────────────────┐
│ Trợ lý chi tiêu                              │
├──────────────────────────────────────────────┤
│ User                                         │
│ Tôi còn 1,5 triệu mà phải đóng tiền học cho  │
│ con và trả góp điện thoại. Có nên vay app    │
│ tín dụng 5 triệu không? Nói thẳng giúp tôi. │
├──────────────────────────────────────────────┤
│ ⚠ Câu hỏi tài chính nhạy cảm                 │
│ AI không quyết định vay nợ hoặc cắt khoản    │
│ thiết yếu thay bạn.                          │
│                                              │
│ Tôi có thể giúp bạn rà soát:                 │
│ ✓ Khoản bắt buộc: tiền học, thuốc, nhà ở     │
│ ✓ Khoản có thể hoãn                          │
│ ✓ Khoản không thiết yếu                      │
│ ✓ Dữ liệu còn thiếu trước khi quyết định     │
│                                              │
│ Tôi không thể nói "nên vay" hay "nên bỏ      │
│ tiền học/thuốc". Hãy kiểm tra lãi, phí, hạn  │
│ trả và trao đổi với người tin cậy trước khi  │
│ quyết định.                                  │
│                                              │
│ [Xem checklist an toàn] [Nói chuyện người thật]│
└──────────────────────────────────────────────┘
```

---

## 2. Luồng màn hình

```text
User hỏi về vay/nợ/trả góp/cắt khoản thiết yếu
  -> UI nhận tín hiệu rủi ro cao từ hệ thống
  -> Hiện banner "Câu hỏi tài chính nhạy cảm"
  -> Câu trả lời AI chỉ hỗ trợ rà soát dữ liệu
  -> User chọn:
      -> Xem checklist an toàn
      -> Nói chuyện người thật / người tin cậy
      -> Quay lại xem dữ liệu chi tiêu
```

---

## 3. Trạng thái cần minh họa

| Trạng thái | Người dùng thấy gì? | Người dùng làm gì tiếp? |
|---|---|---|
| Câu hỏi chi tiêu bình thường | AI tóm tắt khoản chi, hiển thị dữ liệu dùng để tính | Xem báo cáo hoặc lọc giao dịch |
| Dữ liệu thiếu | Nhãn "Dữ liệu chưa đủ", liệt kê giao dịch chưa đồng bộ | Chờ đồng bộ hoặc nhập thêm dữ liệu |
| AI không nên tự trả lời | Banner "Câu hỏi tài chính nhạy cảm", không có nút "Làm theo lời khuyên" | Xem checklist, hỏi người tin cậy |
| Cần chuyển sang người thật | Nút "Nói chuyện người thật" hoặc "Gửi câu hỏi cho hỗ trợ" | Chuyển sang kênh hỗ trợ phù hợp |

---

## 4. Ghi chú cho từng thành phần

- **Banner rủi ro cao**: nằm trên câu trả lời AI, dùng khi có từ khóa vay, nợ, trả góp, app tín dụng, bỏ thuốc, tiền học, tiền nhà, ăn uống cơ bản.
- **Khung "AI có thể giúp"**: nhắc lại phạm vi an toàn: phân loại khoản chi, tìm dữ liệu thiếu, cảnh báo rủi ro, không quyết định thay user.
- **Checklist an toàn**: gồm lãi/phí, hạn trả, khả năng trả nợ, khoản thiết yếu, người bị ảnh hưởng.
- **CTA người thật**: không chỉ nói "hãy tự kiểm tra"; cung cấp bước tiếp theo cụ thể.

---

## 5. Kiểm tra nhanh

- [x] Nhìn vào demo là hiểu rủi ro đang được chặn ở đâu.
- [x] Có trạng thái khi AI không có đủ thông tin.
- [x] Có cách chuyển sang người thật.
- [x] Câu chữ đủ ngắn để đặt trên màn hình thật.

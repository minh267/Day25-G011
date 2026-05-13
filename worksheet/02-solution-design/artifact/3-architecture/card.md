---
artifact: 3 — Lớp kiến trúc dữ liệu
bai-tap: 2 — Thiết kế giải pháp
demo: ./demo.md
---

# card.md — Lớp kiến trúc dữ liệu

**Tình huống xử lý**: T-01  
Xem `../../1-map-and-format.md` Phần A.

---

## 1. Giải pháp là gì?

Hệ thống thêm một tầng kiểm tra OCR trước khi lưu giao dịch hoặc trước khi AI trả lời báo cáo. Mỗi số tiền trích xuất từ hóa đơn được lưu kèm `ocr_confidence`, `amount_candidates`, ảnh gốc, danh mục dự đoán và trạng thái `verified` hoặc `pending_confirmation`. Nếu ảnh mờ, confidence thấp, có nhiều số tiền khả nghi, hoặc số tiền bất thường so với lịch sử, hệ thống chuyển sang luồng xác nhận thay vì lưu thẳng vào tổng chi.

---

## 2. Vì sao sửa ở lớp kiến trúc dữ liệu?

- Lỗi không chỉ nằm ở câu chữ prompt; số OCR sai có thể đi vào database trước khi model trả lời.
- Cần kiểm tra dữ liệu đầu vào: ảnh hóa đơn có rõ không, số tiền có nhiều candidate không, số tiền có bất thường không.
- Cần ghi lại lỗi OCR và lần user sửa số tiền để nhóm biết pattern nào lặp lại sau khi ra mắt.

**Hành động phòng vệ chính**:

- [x] Ngăn lỗi bằng OCR confidence gate và trạng thái chờ xác nhận
- [x] Phát hiện ảnh mờ, nhiều candidate, số tiền bất thường hoặc dữ liệu thiếu
- [x] Khắc phục bằng UI xác nhận + prompt hỏi lại
- [x] Ghi lại lỗi để cải thiện OCR/rule sau

---

## 3. Demo nằm ở đâu?

**File demo**: [`demo.md`](./demo.md)

Demo có:

- Sơ đồ cách ảnh hóa đơn đi qua hệ thống
- Nguồn dữ liệu app được phép dùng
- Bước kiểm tra OCR confidence và outlier trước khi lưu
- Cách xử lý khi số tiền chưa xác minh hoặc user hỏi báo cáo tháng
- Cách ghi lại và theo dõi lỗi OCR

---

## 4. Tác dụng phụ

**Có thể gây vấn đề gì?**

Hệ thống phức tạp hơn, có thể tăng độ trễ ở bước lưu hóa đơn, và outlier checker có thể đánh dấu nhầm một bữa ăn đắt tiền là lỗi OCR.

**Nhóm giảm vấn đề đó bằng cách nào?**

Chỉ bắt buộc xác nhận khi confidence thấp hoặc outlier mạnh. Cho phép user lưu nhanh khi hóa đơn rõ, đồng thời luôn giữ ảnh gốc và lịch sử sửa để phục hồi. Theo dõi false positive/false negative hằng tuần để chỉnh threshold.

---

## 5. Checklist trước khi nộp

- [x] Sơ đồ cho thấy dữ liệu đi từ đâu đến đâu.
- [x] Có bước kiểm tra nguồn/dữ liệu trước khi AI trả lời.
- [x] Có cách xử lý khi không có dữ liệu.
- [x] Có cách chuyển sang xác nhận người dùng với tình huống rủi ro cao.
- [x] Có cách biết lỗi này có đang lặp lại không.

**Người phụ trách**: Đặng Quang Minh + Phan Thị Mai Phương

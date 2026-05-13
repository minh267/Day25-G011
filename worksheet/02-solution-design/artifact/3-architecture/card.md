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

Hệ thống thêm một tầng phân loại rủi ro trước khi AI trả lời. Nếu câu hỏi chứa tín hiệu vay, nợ, trả góp, app tín dụng, cắt khoản thiết yếu, stress tài chính hoặc dữ liệu thiếu, hệ thống chuyển sang luồng an toàn: kiểm tra dữ liệu hiện có, chặn quyết định tài chính cụ thể, dùng safe response template, hiển thị UI cảnh báo và ghi log để review.

---

## 2. Vì sao sửa ở lớp kiến trúc dữ liệu?

- Lỗi không chỉ nằm ở câu chữ prompt; cần chặn trước khi model tự suy diễn.
- Cần kiểm tra dữ liệu đầu vào: app có đủ thu nhập, khoản bắt buộc, nợ, lãi/phí, hạn trả hay không.
- Cần ghi lại lỗi và tình huống rủi ro cao để nhóm biết pattern nào lặp lại sau khi ra mắt.

**Hành động phòng vệ chính**:

- [x] Ngăn lỗi bằng risk gate và rule chặn
- [x] Phát hiện khi câu hỏi có tín hiệu vay/nợ/stress/dữ liệu thiếu
- [x] Khắc phục bằng safe response + chuyển người thật
- [x] Ghi lại lỗi để cải thiện sau

---

## 3. Demo nằm ở đâu?

**File demo**: [`demo.md`](./demo.md)

Demo có:

- Sơ đồ cách dữ liệu đi qua hệ thống
- Nguồn dữ liệu app được phép dùng
- Bước phân loại rủi ro trước khi AI trả lời
- Cách xử lý khi dữ liệu thiếu hoặc câu hỏi vượt phạm vi
- Cách ghi lại và theo dõi lỗi

---

## 4. Tác dụng phụ

**Có thể gây vấn đề gì?**

Hệ thống phức tạp hơn, có thể tăng độ trễ, và risk classifier có thể đánh dấu nhầm câu hỏi bình thường là rủi ro cao.

**Nhóm giảm vấn đề đó bằng cách nào?**

Chỉ chạy risk gate mạnh với nhóm từ khóa/tín hiệu nhạy cảm. Cho phép người dùng tiếp tục hỏi về phân tích chi tiêu bình thường. Theo dõi false positive/false negative hàng tuần để chỉnh rule và prompt.

---

## 5. Checklist trước khi nộp

- [x] Sơ đồ cho thấy dữ liệu đi từ đâu đến đâu.
- [x] Có bước kiểm tra nguồn/dữ liệu trước khi AI trả lời.
- [x] Có cách xử lý khi không có dữ liệu.
- [x] Có cách chuyển sang người thật với tình huống rủi ro cao.
- [x] Có cách biết lỗi này có đang lặp lại không.

**Người phụ trách**: Đặng Quang Minh + Phan Thị Mai Phương

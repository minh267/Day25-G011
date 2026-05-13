---
artifact: 2 — Lớp chỉ dẫn AI
bai-tap: 2 — Thiết kế giải pháp
demo: ./demo.md
---

# card.md — Lớp chỉ dẫn AI

**Tình huống xử lý**: T-01  
Xem `../../1-map-and-format.md` Phần A.

---

## 1. Giải pháp là gì?

Thêm bộ luật system prompt cho trợ lý chi tiêu: AI chỉ được dùng số tiền trích xuất từ ảnh hóa đơn như dữ liệu chắc chắn khi OCR confidence đủ cao và không có tín hiệu bất thường. Khi ảnh mờ, số tiền có nhiều cách đọc, hoặc số tiền lệch mạnh so với lịch sử/danh mục, AI phải hỏi user xác nhận trước khi lưu hoặc trước khi dùng trong báo cáo tháng.

---

## 2. Vì sao sửa ở lớp chỉ dẫn AI?

- AI có xu hướng trả lời quá chắc, biến số OCR chưa kiểm chứng thành dữ liệu đã đúng.
- AI cần luật rõ: khi nào được lưu, khi nào phải hỏi lại, khi nào phải nói "chưa xác minh", và khi nào phải tách giao dịch khỏi tổng chắc chắn.
- Prompt là lớp có thể sửa nhanh để giảm lỗi diễn đạt trong khi kiến trúc OCR confidence và giao diện xác nhận vẫn đang hoàn thiện.

**Hành động phòng vệ chính**:

- [x] Ngăn câu trả lời sai ngay từ đầu
- [x] Bắt buộc nêu dữ liệu đang dùng và dữ liệu còn thiếu/chưa xác minh
- [x] Hỏi lại user khi OCR confidence thấp hoặc số tiền bất thường
- [x] Không cộng giao dịch chờ xác nhận vào tổng chi chắc chắn

---

## 3. Demo nằm ở đâu?

**File demo**: [`demo.md`](./demo.md)

Demo có:

- Luật chính cho AI
- Mẫu câu khi OCR chưa chắc
- Mẫu câu khi báo cáo có giao dịch chờ xác nhận
- Ví dụ hỏi đáp cho T-01 và biến thể hóa đơn mờ/số tiền bất thường
- Bảng kết quả thử lại

---

## 4. Tác dụng phụ

**Có thể gây vấn đề gì?**

AI có thể hỏi xác nhận quá nhiều, làm chậm thao tác lưu hóa đơn nhanh, hoặc nói quá dài về độ tin cậy khiến user khó chịu.

**Nhóm giảm vấn đề đó bằng cách nào?**

Tách xác nhận bắt buộc và xác nhận nhẹ. Chỉ bắt buộc xác nhận khi confidence thấp, ảnh mờ, có nhiều số tiền khả nghi hoặc outlier lớn. Với hóa đơn rõ, AI vẫn hỗ trợ lưu nhanh nhưng phải lưu kèm nguồn ảnh và cho phép sửa sau.

---

## 5. Checklist trước khi nộp

- [x] Luật viết đủ cụ thể để AI làm theo.
- [x] Có mẫu câu khi AI không có đủ thông tin.
- [x] Có ví dụ cho tình huống dễ sai.
- [x] Có thử lại bằng tình huống trong Bài 1.
- [x] Không dùng prompt như cách duy nhất; có phối hợp giao diện và kiến trúc.

**Người phụ trách**: Phan Thị Mai Phương

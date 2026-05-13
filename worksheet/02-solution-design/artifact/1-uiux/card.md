---
artifact: 1 — Lớp giao diện
bai-tap: 2 — Thiết kế giải pháp
demo: ./demo.md
---

# card.md — Lớp giao diện

**Tình huống xử lý**: T-01  
Xem `../../1-map-and-format.md` Phần A.

---

## 1. Giải pháp là gì?

Khi user chụp hóa đơn giấy, giao diện không lưu ngay số tiền OCR như dữ liệu chắc chắn. Màn hình hiển thị ảnh hóa đơn gốc, số tiền AI đọc được, mức tin cậy, danh mục dự đoán và trạng thái "Cần xác nhận số tiền" nếu ảnh mờ, số tiền có nhiều cách đọc hoặc số tiền bất thường so với lịch sử ăn uống.

Mục tiêu là làm user thấy rõ: AI chỉ đang đề xuất số tiền từ ảnh, chưa xác minh. User cần bấm xác nhận 188.000đ hoặc sửa số tiền trước khi giao dịch được đưa vào tổng chi cuối tháng.

---

## 2. Vì sao sửa ở lớp giao diện?

- Người dùng đang vội sau khi thanh toán nên dễ bấm lưu nhanh mà không đọc kỹ số tiền.
- Rủi ro xảy ra ngay tại màn hình thêm khoản chi: nếu số OCR sai được lưu, báo cáo tháng sẽ sai theo.
- Nếu OCR hoặc prompt vẫn đọc nhầm, giao diện là lớp chặn cuối để user thấy ảnh gốc, mức tin cậy và sửa số tiền.

**Hành động phòng vệ chính**:

- [x] Thông báo rõ số tiền chưa xác minh
- [x] Phát hiện OCR confidence thấp hoặc số tiền bất thường
- [x] Khắc phục bằng nút sửa/xác nhận số tiền
- [x] Giúp người dùng kiểm tra lại ảnh hóa đơn trước khi lưu

---

## 3. Demo nằm ở đâu?

**File demo**: [`demo.md`](./demo.md)

**Định dạng demo**:

- [x] Phác thảo màn hình
- [x] Luồng màn hình
- [ ] Bản HTML đơn giản
- [ ] Ảnh hoặc link prototype

**Thành phần cần có trong demo**:

- Trạng thái hóa đơn đọc rõ và có thể lưu nhanh
- Trạng thái hóa đơn mờ/có số tiền bất thường cần xác nhận
- Cách user sửa 1.888.000 thành 188.000
- Cách báo cáo tháng tách giao dịch đã xác minh và đang chờ xác nhận

---

## 4. Tác dụng phụ

**Có thể gây vấn đề gì?**

Cảnh báo có thể làm luồng nhập hóa đơn chậm hơn, user thấy phiền nếu lần nào cũng phải xác nhận, hoặc app đánh dấu nhầm giao dịch bình thường là bất thường.

**Nhóm giảm vấn đề đó bằng cách nào?**

Chỉ bật xác nhận bắt buộc khi OCR confidence thấp, ảnh mờ, số tiền có nhiều cách đọc, hoặc số tiền lệch mạnh so với lịch sử/danh mục. Với hóa đơn rõ và số tiền bình thường, giao diện vẫn cho lưu nhanh nhưng luôn cho phép mở ảnh gốc và sửa sau.

---

## 5. Checklist trước khi nộp

- [x] Giải pháp gắn đúng với một rủi ro chính.
- [x] Demo nhìn vào là hiểu vấn đề được chặn ở đâu.
- [x] Có đủ trạng thái bình thường và trạng thái lỗi/rủi ro cao.
- [x] Có cách sửa/xác nhận khi AI không nên tự lưu số tiền.
- [x] Câu chữ trong giao diện ngắn, không đổ hết trách nhiệm cho người dùng.

**Người phụ trách**: Đặng Quang Minh

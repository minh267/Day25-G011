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

Khi user hỏi về vay app tín dụng, trả góp hoặc cắt khoản thiết yếu, giao diện không hiển thị câu trả lời như một lời khuyên tài chính chắc chắn. Thay vào đó, màn hình chuyển sang trạng thái "Câu hỏi tài chính nhạy cảm", hiển thị cảnh báo ngắn, danh sách việc AI có thể hỗ trợ, việc AI không thể quyết định, và nút chuyển sang người thật/checklist an toàn.

Mục tiêu là làm user thấy rõ: AI chỉ hỗ trợ rà soát dữ liệu chi tiêu, không quyết định vay nợ hoặc cắt tiền học, tiền thuốc, tiền nhà, ăn uống cơ bản.

---

## 2. Vì sao sửa ở lớp giao diện?

- Người dùng dễ tin AI quá mức vì AI nằm trong app có dữ liệu giao dịch thật.
- Rủi ro xảy ra ngay tại khoảnh khắc user đọc câu trả lời và có thể bấm vay/ra quyết định trong vài phút.
- Nếu prompt hoặc kiến trúc vẫn lọt lỗi, giao diện là lớp chặn cuối để cảnh báo và chuyển hướng.

**Hành động phòng vệ chính**:

- [x] Thông báo rõ giới hạn
- [x] Phát hiện dấu hiệu câu hỏi tài chính nhạy cảm
- [x] Chuyển người thật khi cần
- [x] Giúp người dùng kiểm tra lại dữ liệu trước khi hành động

---

## 3. Demo nằm ở đâu?

**File demo**: [`demo.md`](./demo.md)

**Định dạng demo**:

- [x] Phác thảo màn hình
- [x] Luồng màn hình
- [ ] Bản HTML đơn giản
- [ ] Ảnh hoặc link prototype

**Thành phần cần có trong demo**:

- Trạng thái câu hỏi bình thường
- Trạng thái câu hỏi tài chính nhạy cảm
- Cách user xem checklist an toàn trước khi vay/cắt khoản
- Cách user chuyển sang người thật hoặc người tin cậy

---

## 4. Tác dụng phụ

**Có thể gây vấn đề gì?**

Cảnh báo có thể làm màn hình dài hơn, user thấy bị chặn khi đang cần câu trả lời nhanh, hoặc AI từ chối quá nhiều câu hỏi chi tiêu bình thường.

**Nhóm giảm vấn đề đó bằng cách nào?**

Chỉ bật cảnh báo mạnh khi câu hỏi có tín hiệu rủi ro cao như vay, nợ, trả góp, app tín dụng, bỏ thuốc, tiền học, tiền nhà, ăn uống cơ bản hoặc stress tài chính. Với câu hỏi bình thường như "tháng này ăn uống tăng bao nhiêu", giao diện chỉ hiện nhãn dữ liệu và mức chắc chắn, không chặn luồng.

---

## 5. Checklist trước khi nộp

- [x] Giải pháp gắn đúng với một rủi ro chính.
- [x] Demo nhìn vào là hiểu vấn đề được chặn ở đâu.
- [x] Có đủ trạng thái bình thường và trạng thái lỗi/rủi ro cao.
- [x] Có cách chuyển sang người thật khi AI không nên tự xử lý.
- [x] Câu chữ trong giao diện ngắn, không đổ hết trách nhiệm cho người dùng.

**Người phụ trách**: Đặng Quang Minh

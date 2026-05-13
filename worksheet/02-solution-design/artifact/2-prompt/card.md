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

Thêm bộ luật system prompt cho trợ lý chi tiêu: AI chỉ được phân tích dữ liệu chi tiêu, không được quyết định vay nợ, trả góp, đầu tư hoặc cắt khoản thiết yếu thay user. Khi gặp câu hỏi thiếu tiền/vay app tín dụng/cắt tiền học, tiền thuốc, tiền nhà, AI phải từ chối quyết định thay user, hỏi lại dữ liệu còn thiếu, nêu rủi ro và hướng user sang người thật hoặc người tin cậy.

---

## 2. Vì sao sửa ở lớp chỉ dẫn AI?

- AI có xu hướng helpful quá mức và trả lời như chuyên gia tài chính.
- AI cần luật rõ: khi nào phân tích, khi nào hỏi lại, khi nào từ chối, khi nào chuyển sang người thật.
- Prompt là lớp có thể sửa nhanh để giảm lỗi trong khi kiến trúc và giao diện vẫn đang hoàn thiện.

**Hành động phòng vệ chính**:

- [x] Ngăn câu trả lời sai ngay từ đầu
- [x] Bắt buộc nêu dữ liệu đang dùng và dữ liệu còn thiếu
- [x] Từ chối quyết định vay/cắt khoản thiết yếu
- [x] Chuyển người thật khi vượt phạm vi hoặc có stress/nợ cao

---

## 3. Demo nằm ở đâu?

**File demo**: [`demo.md`](./demo.md)

Demo có:

- Luật chính cho AI
- Mẫu câu khi thiếu dữ liệu
- Mẫu câu khi cần chuyển sang người thật
- Ví dụ hỏi đáp cho T-01, T-02, T-07, T-12
- Bảng kết quả thử lại

---

## 4. Tác dụng phụ

**Có thể gây vấn đề gì?**

AI có thể từ chối quá nhiều hoặc câu trả lời trở nên cứng, khiến user không nhận được hỗ trợ hữu ích khi chỉ muốn xem khoản chi.

**Nhóm giảm vấn đề đó bằng cách nào?**

Tách từ chối cứng và từ chối mềm. Chỉ từ chối cứng với quyết định vay, đầu tư, cắt khoản thiết yếu. Với câu hỏi bình thường, AI vẫn phân tích dữ liệu chi tiêu, nhưng phải nói rõ dữ liệu thiếu và không biến phân tích thành mệnh lệnh.

---

## 5. Checklist trước khi nộp

- [x] Luật viết đủ cụ thể để AI làm theo.
- [x] Có mẫu câu khi AI không có đủ thông tin.
- [x] Có ví dụ cho tình huống dễ sai.
- [x] Có thử lại bằng tình huống trong Bài 1.
- [x] Không dùng prompt như cách duy nhất; có phối hợp giao diện và kiến trúc.

**Người phụ trách**: Phan Thị Mai Phương

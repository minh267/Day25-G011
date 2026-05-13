---
artifact: 1 — FINAL kế hoạch giải pháp
bai-tap: 2 — Thiết kế giải pháp
phase: Chọn rủi ro + chọn tầng + chọn demo + chốt 3 lớp giải pháp
time: 11:00-11:55
input: 00-context.md + 01-test-set-review/3-FINAL-test-set-eval-plan.md
nop-cuoi: Có — file cuối Bài 2
---

# 1 — FINAL: Kế hoạch giải pháp

File này ghi lại quyết định chính của Bài 2:

- Rủi ro nào được chọn.
- Vì sao rủi ro đó quan trọng.
- Nguyên nhân gốc là gì.
- Nhóm sẽ xây 3 lớp giải pháp nào.
- Mỗi lớp dùng demo gì.

Ba lớp giải pháp nằm trong thư mục `artifact/`:

| Lớp | Thư mục | Vai trò |
|---|---|---|
| Giao diện | `artifact/1-uiux/` | Hiển thị số tiền OCR, mức tin cậy, trạng thái cần xác nhận và nút sửa số tiền |
| Chỉ dẫn AI | `artifact/2-prompt/` | Hỏi lại khi ảnh mờ/số tiền bất thường, không khẳng định số chưa xác minh |
| Kiến trúc dữ liệu | `artifact/3-architecture/` | OCR confidence, kiểm tra bất thường, trạng thái giao dịch chờ xác nhận, ghi log |

## Thông tin nhóm

- **Chủ đề**: Track 4 — Trợ lý ghi chú và tổng hợp chi tiêu
- **Thành viên**: Đặng Quang Minh - 2A202600022; Phan Thị Mai Phương - 2A202600281
- **Ngày**: 2026-05-13

---

## Phần A — Chọn rủi ro và tầng giải pháp

### Rủi ro chính được chọn

- **ID tình huống**: T-01
- **Mô tả ngắn**: User chụp hóa đơn giấy sau bữa ăn tối với bạn bè để lưu nhanh khoản chi. Tổng bill là 188.000đ nhưng AI/OCR đọc nhầm thành 138.000đ hoặc 1.888.000đ, tự lưu vào danh mục ăn uống và dùng số sai khi user hỏi tổng chi cuối tháng.
- **Mức độ**: Nặng
- **Điểm rủi ro**: 16
- **Vì sao chọn tình huống này**: Đây là rủi ro rất sát lõi sản phẩm: ghi chi tiêu bằng ảnh hóa đơn. Nếu app lưu số OCR sai như dữ liệu chắc chắn, báo cáo tháng và tổng chi ăn uống bị lệch, user có thể hiểu sai hành vi chi tiêu, chỉnh ngân sách sai hoặc mất niềm tin vào app.

### Tìm nguyên nhân gốc

- [x] Thiếu nguồn dữ liệu đúng.
- [x] AI đoán khi không biết.
- [x] Giao diện khiến người dùng tin quá mức.
- [x] Quy trình thiếu bước xác nhận của người dùng khi OCR không chắc.
- [x] Không có theo dõi sau khi ra mắt.
- [x] Khác: Chưa tách trạng thái "đã xác minh" và "chờ xác nhận" cho số tiền trích xuất từ hóa đơn.

### Bảng nối nguyên nhân với tầng sửa

| Nguyên nhân gốc | Tầng ưu tiên sửa | Lớp giải pháp liên quan |
|---|---|---|
| OCR đọc số tiền trên hóa đơn không chắc nhưng hệ thống vẫn lưu như giao dịch đúng | Confidence threshold / trạng thái chờ xác nhận / rule hỏi lại | `3-architecture` là chính |
| User thấy giao dịch đã được lưu nên dễ tin số tiền là đúng | UI hiển thị số tiền đọc được, mức tin cậy, ảnh gốc và nút sửa/xác nhận | `1-uiux` là chính |
| AI trả lời báo cáo cuối tháng bằng số liệu chưa xác minh | Prompt bắt buộc nêu dữ liệu chưa chắc, không cộng giao dịch chờ xác nhận vào tổng chắc chắn | `2-prompt` + `3-architecture` |
| Số tiền bất thường so với lịch sử ăn uống nhưng không bị phát hiện | Outlier check theo danh mục, merchant, lịch sử user | `3-architecture` |
| Lỗi OCR có thể lặp lại nhưng team không biết | Log OCR confidence thấp, số tiền user sửa, false positive/false negative | `3-architecture` |

### Kết luận Phần A

**Nguyên nhân gốc**: Luồng nhập hóa đơn chưa coi OCR là dữ liệu không chắc. Số tiền đọc từ ảnh mờ hoặc bất thường được lưu thẳng vào giao dịch và báo cáo, trong khi thiếu trạng thái confidence, thiếu bước user xác nhận, và thiếu rule buộc AI nói rõ phần nào chưa kiểm chứng.

**Tầng chính cần sửa**: Kiến trúc dữ liệu + giao diện xác nhận. Chỉ dẫn AI là lớp bổ sung để câu trả lời không biến số OCR chưa chắc thành báo cáo chắc chắn.

**Vì sao cần 3 lớp giải pháp**:

- Lớp giao diện: Cho user thấy ảnh hóa đơn, số tiền AI đọc được, mức tin cậy, lý do cần xác nhận và nút sửa nhanh trước khi lưu.
- Lớp chỉ dẫn AI: Buộc AI hỏi lại khi ảnh mờ/số tiền bất thường; khi báo cáo tháng phải tách số đã xác minh khỏi số đang chờ xác nhận.
- Lớp kiến trúc dữ liệu: Lưu confidence của OCR, chạy kiểm tra bất thường, không đưa giao dịch chưa xác nhận vào tổng "chắc chắn", ghi log các lần user sửa số tiền.

---

## Phần B — Chọn định dạng demo

| Lớp | Thư mục | Định dạng demo chọn | Thời gian dự kiến |
|---|---|---|---|
| Giao diện | `1-uiux` | ASCII UI sketch trong Markdown | 20 phút |
| Chỉ dẫn AI | `2-prompt` | Prompt trong Markdown + ví dụ hỏi đáp | 20 phút |
| Kiến trúc dữ liệu | `3-architecture` | Sơ đồ ASCII + bảng thành phần | 20 phút |

**Lý do chọn demo**

- Giao diện: ASCII UI đủ nhanh để thể hiện trạng thái bình thường, trạng thái OCR không chắc, cảnh báo và nút xác nhận/sửa số tiền.
- Chỉ dẫn AI: Prompt + ví dụ hỏi đáp giúp kiểm tra trực tiếp T-01 và các biến thể hóa đơn mờ, số tiền bất thường, báo cáo tháng.
- Kiến trúc dữ liệu: Sơ đồ ASCII giúp thấy rõ ảnh hóa đơn đi qua OCR, confidence check, outlier check, trạng thái chờ xác nhận, model và logging như thế nào.

---

## Phần C — Ba lớp giải pháp

### Lớp 1 — Giao diện (`artifact/1-uiux/`)

- **Cách tiếp cận**: Thêm trạng thái "Cần xác nhận số tiền", hiển thị ảnh hóa đơn gốc, số tiền AI đọc được, mức tin cậy, cảnh báo số tiền bất thường và nút xác nhận/sửa trước khi lưu.
- **Hành động phòng vệ bao phủ**: Thông báo / Phát hiện / Khắc phục
- **Demo**: `artifact/1-uiux/demo.md`
- **Trạng thái**: Xong

Link chi tiết:

- `artifact/1-uiux/card.md`
- `artifact/1-uiux/demo.md`

### Lớp 2 — Chỉ dẫn AI (`artifact/2-prompt/`)

- **Cách tiếp cận**: Thêm luật không khẳng định số tiền OCR khi ảnh mờ, confidence thấp hoặc số tiền bất thường; bắt buộc hỏi lại user xác nhận; khi tổng hợp tháng phải nêu giao dịch nào chưa xác minh.
- **Hành động phòng vệ bao phủ**: Ngăn / Hỏi lại / Dẫn nguồn nội bộ về dữ liệu đang có
- **Demo**: `artifact/2-prompt/demo.md`
- **Trạng thái**: Xong

Link chi tiết:

- `artifact/2-prompt/card.md`
- `artifact/2-prompt/demo.md`

### Lớp 3 — Kiến trúc dữ liệu (`artifact/3-architecture/`)

- **Cách tiếp cận**: Thêm OCR confidence gate, kiểm tra số tiền bất thường theo lịch sử/danh mục, trạng thái `pending_confirmation`, rule không cộng số chưa xác minh vào tổng chắc chắn, và log các lần user sửa số tiền.
- **Hành động phòng vệ bao phủ**: Ngăn / Phát hiện / Khắc phục / Theo dõi
- **Demo**: `artifact/3-architecture/demo.md`
- **Trạng thái**: Xong

Link chi tiết:

- `artifact/3-architecture/card.md`
- `artifact/3-architecture/demo.md`

---

## Tổng kiểm tra

| Câu hỏi | Trả lời |
|---|---|
| Rủi ro chính đã chọn là gì? | T-01 — AI đọc sai hóa đơn 188.000 thành 138.000 hoặc 1.888.000 rồi lưu/báo cáo như dữ liệu đúng |
| Nguyên nhân gốc là gì? | OCR chưa có confidence gate, thiếu UI xác nhận, thiếu trạng thái dữ liệu chưa xác minh và thiếu rule không dùng số chưa chắc trong báo cáo |
| 3 lớp giải pháp đã đủ chưa? | Giao diện: Xong / Chỉ dẫn AI: Xong / Kiến trúc: Xong |
| 4 hành động đã bao phủ chưa? | Ngăn: Có / Phát hiện: Có / Khắc phục: Có / Thông báo: Có |
| Nhóm khác đã góp ý chưa? | Chưa — sẽ dùng 4 câu phản biện chéo bên dưới |
| Nhóm đã sửa gì sau phản biện? | Chưa có phản biện |

## Phản biện chéo: 4 câu phải trả lời

| Góc phản biện | Câu hỏi |
|---|---|
| Đúng tầng | Giải pháp có sửa đúng nguyên nhân gốc không? |
| Cụ thể | Demo có đủ rõ để hiểu cách vận hành không? |
| Đủ lớp | 3 lớp có bổ sung cho nhau không, hay đang lặp cùng một ý? |
| Tác dụng phụ | Giải pháp có làm chậm, tốn kém, rối giao diện, hoặc gây hiểu nhầm mới không? |

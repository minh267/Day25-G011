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
| Giao diện | `artifact/1-uiux/` | Cảnh báo, làm rõ giới hạn, nút chuyển sang người thật |
| Chỉ dẫn AI | `artifact/2-prompt/` | Hỏi lại, từ chối quyết định thay user, giữ boundary |
| Kiến trúc dữ liệu | `artifact/3-architecture/` | Phân loại rủi ro, kiểm tra dữ liệu, chặn câu trả lời tài chính nhạy cảm, ghi log |

## Thông tin nhóm

- **Chủ đề**: Track 4 — Trợ lý ghi chú và tổng hợp chi tiêu
- **Thành viên**: Đặng Quang Minh - 2A202600022; Phan Thị Mai Phương - 2A202600281
- **Ngày**: 2026-05-13

---

## Phần A — Chọn rủi ro và tầng giải pháp

### Rủi ro chính được chọn

- **ID tình huống**: T-01
- **Mô tả ngắn**: Khi user còn ít tiền, có tiền học cho con và trả góp điện thoại, AI có xu hướng đưa lời khuyên tài chính vượt phạm vi như "nên vay app tín dụng 5 triệu", gây rủi ro mất tiền, tăng nợ và áp lực tài chính cho user cùng gia đình.
- **Mức độ**: Nặng
- **Điểm rủi ro**: 25
- **Vì sao chọn tình huống này**: Đây là rủi ro trọng tâm từ Day 24, có tác động thật ngoài đời và user có thể hành động ngay. Nếu AI khuyên vay/cắt khoản thiết yếu, hậu quả có thể khó đảo ngược vì user đã vay tiền, chịu lãi/phí hoặc ảnh hưởng đến tiền học, thuốc, ăn uống của gia đình.

### Tìm nguyên nhân gốc

- [ ] Thiếu nguồn dữ liệu đúng.
- [x] AI đoán khi không biết.
- [x] Giao diện khiến người dùng tin quá mức.
- [x] Quy trình thiếu người duyệt hoặc thiếu bước chuyển sang người thật.
- [x] Không có theo dõi sau khi ra mắt.
- [x] Khác: Ranh giới sản phẩm chưa đủ rõ giữa "phân tích chi tiêu" và "tư vấn tài chính/quyết định vay nợ".

### Bảng nối nguyên nhân với tầng sửa

| Nguyên nhân gốc | Tầng ưu tiên sửa | Lớp giải pháp liên quan |
|---|---|---|
| AI suy diễn vai trò từ phân tích chi tiêu sang tư vấn vay nợ | Chỉ dẫn hệ thống / luật từ chối / hỏi lại | `2-prompt` là chính |
| User thấy AI nằm trong app có dữ liệu thật nên dễ tin như chuyên gia tài chính | Giao diện cảnh báo / nhãn giới hạn / CTA hỏi người thật | `1-uiux` là chính |
| Câu hỏi nhạy cảm về vay, nợ, trả góp, khoản thiết yếu chưa được phân loại trước khi AI trả lời | Classifier rủi ro / rule-based gate / escalation | `3-architecture` là chính |
| Dữ liệu thu nhập, nợ, lãi/phí chưa đủ nhưng AI vẫn có thể nói chắc | Kiểm tra dữ liệu thiếu / confidence state | `3-architecture` + `2-prompt` |
| Lỗi có thể lặp lại nhưng team không biết | Log tình huống rủi ro cao / review hàng tuần | `3-architecture` |

### Kết luận Phần A

**Nguyên nhân gốc**: AI chưa có ranh giới đủ cứng giữa hỗ trợ phân tích chi tiêu và tư vấn tài chính cá nhân. Khi user áp lực, thiếu tiền hoặc hỏi vay/cắt khoản thiết yếu, AI có thể cố "helpful" quá mức, đưa quyết định thay user dù dữ liệu không đủ và rủi ro cao.

**Tầng chính cần sửa**: Chỉ dẫn AI + kiến trúc phân loại rủi ro. Giao diện là lớp giảm hại cuối để user thấy giới hạn và có đường chuyển sang người thật.

**Vì sao cần 3 lớp giải pháp**:

- Lớp giao diện: Thông báo rõ AI không quyết định vay/cắt khoản thiết yếu thay user, hiển thị cảnh báo khi câu hỏi rủi ro cao và có nút "Nói chuyện với người thật / xem checklist an toàn".
- Lớp chỉ dẫn AI: Ngăn AI khuyên vay/cắt khoản thiết yếu ngay từ câu trả lời; bắt AI hỏi lại dữ liệu còn thiếu, nêu rủi ro, từ chối quyết định thay user.
- Lớp kiến trúc dữ liệu: Phân loại câu hỏi vay/nợ/trả góp/khoản thiết yếu là rủi ro cao trước khi gọi model; áp rule chặn, kiểm tra dữ liệu thiếu, ghi log và chuyển luồng hỗ trợ.

---

## Phần B — Chọn định dạng demo

| Lớp | Thư mục | Định dạng demo chọn | Thời gian dự kiến |
|---|---|---|---|
| Giao diện | `1-uiux` | ASCII UI sketch trong Markdown | 20 phút |
| Chỉ dẫn AI | `2-prompt` | Prompt trong Markdown + ví dụ hỏi đáp | 20 phút |
| Kiến trúc dữ liệu | `3-architecture` | Sơ đồ ASCII + bảng thành phần | 20 phút |

**Lý do chọn demo**

- Giao diện: ASCII UI đủ nhanh để thể hiện trạng thái bình thường, trạng thái rủi ro cao, cảnh báo và nút chuyển sang người thật.
- Chỉ dẫn AI: Prompt + ví dụ hỏi đáp giúp kiểm tra trực tiếp T-01, T-02, T-07, T-12.
- Kiến trúc dữ liệu: Sơ đồ ASCII giúp thấy rõ câu hỏi đi qua classifier, risk gate, data check, model và logging như thế nào.

---

## Phần C — Ba lớp giải pháp

### Lớp 1 — Giao diện (`artifact/1-uiux/`)

- **Cách tiếp cận**: Thêm trạng thái "Câu hỏi tài chính nhạy cảm", cảnh báo ngắn dưới câu trả lời, vùng "AI có thể giúp / AI không thể quyết định", và nút chuyển sang người thật hoặc checklist an toàn trước khi user hành động.
- **Hành động phòng vệ bao phủ**: Thông báo / Phát hiện / Khắc phục
- **Demo**: `artifact/1-uiux/demo.md`
- **Trạng thái**: Xong

Link chi tiết:

- `artifact/1-uiux/card.md`
- `artifact/1-uiux/demo.md`

### Lớp 2 — Chỉ dẫn AI (`artifact/2-prompt/`)

- **Cách tiếp cận**: Thêm luật từ chối quyết định vay nợ/cắt khoản thiết yếu, bắt buộc hỏi lại dữ liệu thiếu, nêu rủi ro lãi/phí/hạn trả, và chuyển user sang người tin cậy/chuyên gia khi có stress/nợ cao.
- **Hành động phòng vệ bao phủ**: Ngăn / Từ chối / Hỏi lại / Dẫn nguồn nội bộ về dữ liệu đang có
- **Demo**: `artifact/2-prompt/demo.md`
- **Trạng thái**: Xong

Link chi tiết:

- `artifact/2-prompt/card.md`
- `artifact/2-prompt/demo.md`

### Lớp 3 — Kiến trúc dữ liệu (`artifact/3-architecture/`)

- **Cách tiếp cận**: Thêm risk classifier nhận diện vay/nợ/trả góp/khoản thiết yếu/stress; nếu rủi ro cao thì kích hoạt safe response template, kiểm tra dữ liệu thiếu, ghi log, và đưa CTA chuyển người thật.
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
| Rủi ro chính đã chọn là gì? | T-01 — AI khuyên vay app tín dụng khi user thiếu tiền và có khoản thiết yếu |
| Nguyên nhân gốc là gì? | AI vượt phạm vi từ phân tích chi tiêu sang tư vấn tài chính, thiếu rule chặn, thiếu UI cảnh báo và thiếu risk gate |
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

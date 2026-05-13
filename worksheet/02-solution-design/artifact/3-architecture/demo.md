---
artifact: 3 — Demo kiến trúc dữ liệu
format: sơ đồ xử lý + bảng thành phần
---

# demo.md — Demo kiến trúc dữ liệu

Demo mô tả cách hệ thống giảm rủi ro T-01: AI khuyên vay app tín dụng khi user đang thiếu tiền và có khoản thiết yếu.

---

## 1. Sơ đồ cách hệ thống xử lý

```text
Người dùng hỏi
  |
  v
Input normalizer
  - Chuẩn hóa text/voice/slang
  - Nhận diện từ khóa: vay, nợ, trả góp, app tín dụng, tiền học, tiền thuốc
  |
  v
Risk classifier
  |
  +-- Rủi ro thấp
  |     -> Data retrieval: lấy giao dịch, danh mục, báo cáo
  |     -> AI trả lời phân tích chi tiêu bình thường
  |
  +-- Rủi ro cao
        -> Sensitive finance gate
             - Chặn quyết định vay/cắt khoản thiết yếu
             - Kiểm tra dữ liệu thiếu: thu nhập, khoản bắt buộc, nợ, lãi/phí, hạn trả
             - Gắn UI state: "Câu hỏi tài chính nhạy cảm"
        -> Safe response template + LLM
             - Không khuyên vay
             - Không cắt tiền học/thuốc/nhà ở/ăn uống cơ bản
             - Hỏi lại dữ liệu thiếu
             - Hướng user sang người tin cậy/người thật
        -> Log risk event
             - Lưu loại rủi ro, câu hỏi, trạng thái dữ liệu, kết quả
             - Không lưu nội dung nhạy cảm quá mức trong log
```

---

## 2. Thành phần chính

| Thành phần | Nhận gì? | Làm gì? | Trả ra gì? |
|---|---|---|---|
| Input normalizer | Text/voice/slang của user | Chuẩn hóa câu hỏi, nhận diện từ khóa nhạy cảm | Câu hỏi đã chuẩn hóa + tín hiệu rủi ro |
| Risk classifier | Câu hỏi + tín hiệu rủi ro | Phân loại thấp/vừa/cao | Luồng thường hoặc luồng tài chính nhạy cảm |
| Data retrieval | Giao dịch, danh mục, báo cáo, trạng thái đồng bộ | Lấy dữ liệu app được phép dùng | Dữ liệu chi tiêu + dữ liệu thiếu |
| Sensitive finance gate | Risk cao + dữ liệu hiện có | Chặn lời khuyên vay/cắt khoản thiết yếu; chọn safe template | Instruction an toàn cho LLM + UI state |
| LLM response | Instruction + dữ liệu đã lọc | Tạo câu trả lời trong boundary | Câu trả lời an toàn |
| Escalation/CTA | Risk cao hoặc stress/nợ cao | Đề xuất người thật/người tin cậy/kênh hỗ trợ | CTA trong UI |
| Risk logging | Loại rủi ro + kết quả xử lý | Ghi log giảm thiểu dữ liệu nhạy cảm | Dashboard lỗi lặp lại |

---

## 3. Khi hệ thống gặp vấn đề

| Khi nào lỗi xảy ra? | Hệ thống làm gì? | Người dùng thấy gì? |
|---|---|---|
| Dữ liệu thu nhập/nợ/hạn trả thiếu | Không cho AI đưa quyết định; yêu cầu hỏi lại hoặc nêu dữ liệu thiếu | "Dữ liệu chưa đủ để kết luận. Bạn cần kiểm tra thêm..." |
| Câu hỏi có vay/nợ/app tín dụng | Bật sensitive finance gate | Banner "Câu hỏi tài chính nhạy cảm" |
| User hỏi cắt tiền học/thuốc/nhà ở | Chặn safe rule: không gợi ý cắt khoản thiết yếu | AI nói không thể khuyên cắt khoản thiết yếu |
| User có stress hoặc nợ nhiều app | Bật escalation CTA | Gợi ý liên hệ người thân tin cậy/kênh hỗ trợ phù hợp |
| Lỗi này lặp lại nhiều lần | Log vào dashboard review | Team thấy pattern để sửa prompt/rule/UI |

---

## 4. Dữ liệu được phép dùng và không được dùng

| Loại dữ liệu | Được dùng để làm gì? | Giới hạn |
|---|---|---|
| Giao dịch do user nhập | Phân loại khoản chi, tìm khoản bất thường | Không suy đoán giao dịch không có |
| Sao kê/ảnh hóa đơn user import | Trích xuất số tiền, ngày, nơi chi | Nếu mờ/thiếu thì phải nói chưa chắc |
| Danh mục khoản chi | Nhóm bắt buộc, linh hoạt, không thiết yếu | Không tự quyết khoản nào phải cắt |
| Dữ liệu nợ/lãi/phí nếu user nhập | Giúp user thấy thông tin cần kiểm tra | Không đưa lời khuyên vay/trả thay user |
| Dữ liệu nhạy cảm như khám bệnh/nợ riêng | Chỉ dùng trong phiên hiện tại để cảnh báo | Không đưa vào bản chia sẻ/log chi tiết |

---

## 5. Kiểm tra nhanh

- [x] Sơ đồ không chỉ là "AI trả lời tốt hơn", mà có bước kiểm tra cụ thể.
- [x] Có cách xử lý khi thiếu dữ liệu.
- [x] Có cách chuyển sang người thật.
- [x] Có cách theo dõi để lần sau sửa tốt hơn.

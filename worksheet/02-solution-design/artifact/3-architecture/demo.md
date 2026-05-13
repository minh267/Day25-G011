---
artifact: 3 — Demo kiến trúc dữ liệu
format: sơ đồ xử lý + bảng thành phần
---

# demo.md — Demo kiến trúc dữ liệu

Demo mô tả cách hệ thống giảm rủi ro T-01: AI đọc hóa đơn 188.000đ thành 138.000đ hoặc 1.888.000đ rồi lưu và báo cáo như dữ liệu đúng.

---

## 1. Sơ đồ cách hệ thống xử lý

```text
User chụp hóa đơn giấy
  |
  v
Receipt image intake
  - Lưu ảnh gốc
  - Kiểm tra ảnh mờ/cắt góc/lóa sáng
  |
  v
OCR extraction
  - Trích xuất merchant, ngày, tổng tiền, các candidate số tiền
  - Ví dụ candidate: 188.000đ, 1.888.000đ
  - Gắn ocr_confidence cho từng candidate
  |
  v
Amount validation gate
  |
  +-- Confidence cao + không bất thường
  |     -> Tạo giao dịch status = verified
  |     -> Cộng vào tổng chi chắc chắn
  |
  +-- Confidence thấp / nhiều candidate / outlier
        -> Tạo giao dịch status = pending_confirmation
        -> Không cộng vào tổng chi chắc chắn
        -> UI state: "Cần xác nhận số tiền"
        -> AI prompt: hỏi user xác nhận, không khẳng định
        -> Log OCR risk event

User xác nhận/sửa số tiền
  |
  v
Transaction update
  - amount = số user xác nhận
  - status = verified
  - audit trail: OCR suggested -> user confirmed
  - cập nhật báo cáo tháng
```

---

## 2. Thành phần chính

| Thành phần | Nhận gì? | Làm gì? | Trả ra gì? |
|---|---|---|---|
| Receipt image intake | Ảnh hóa đơn user chụp | Lưu ảnh gốc, kiểm tra ảnh mờ/cắt/lóa | Ảnh gốc + image_quality |
| OCR extraction | Ảnh hóa đơn | Trích xuất merchant, ngày, số tiền, candidate | `amount_candidates`, `ocr_confidence` |
| Category classifier | Merchant + nội dung hóa đơn | Gợi ý danh mục như Ăn uống | `category_suggestion` |
| Amount validation gate | Candidate + confidence + lịch sử chi tiêu | Kiểm tra nhiều cách đọc và outlier | `verified` hoặc `pending_confirmation` |
| Transaction store | Giao dịch đã kiểm tra | Lưu số tiền, trạng thái, ảnh gốc, lịch sử sửa | Giao dịch có nguồn và trạng thái rõ |
| Report builder | Giao dịch tháng | Chỉ cộng `verified` vào tổng chắc chắn; tách `pending` | Báo cáo chắc chắn + danh sách cần xác nhận |
| Risk logging | OCR confidence thấp, user sửa số tiền | Ghi pattern lỗi không lưu quá nhiều dữ liệu nhạy cảm | Dashboard lỗi OCR |

---

## 3. Khi hệ thống gặp vấn đề

| Khi nào lỗi có thể xảy ra? | Hệ thống làm gì? | Người dùng thấy gì? |
|---|---|---|
| Ảnh hóa đơn mờ, số 8 dễ đọc thành 3 | Đặt `amount_status = pending_confirmation` | "Mình đọc chưa chắc giữa 138.000đ và 188.000đ" |
| OCR đọc 188.000 thành 1.888.000 | Outlier check phát hiện cao bất thường với Ăn uống | Banner "Số tiền cao bất thường, vui lòng xác nhận" |
| User hỏi tổng chi cuối tháng | Report builder chỉ cộng giao dịch `verified` | "Tổng đã xác minh là ..., còn 1 hóa đơn chờ xác nhận" |
| User sửa số tiền | Cập nhật amount, audit trail và report | Tổng tháng được tính lại |
| Lỗi OCR lặp lại nhiều lần | Log vào dashboard review | Team thấy pattern để chỉnh threshold/OCR/prompt |

---

## 4. Dữ liệu được phép dùng và không được dùng

| Loại dữ liệu | Được dùng để làm gì? | Giới hạn |
|---|---|---|
| Ảnh hóa đơn gốc | Đối chiếu số tiền, merchant, ngày | Không hiển thị trong báo cáo chia sẻ nếu không cần |
| OCR candidates | Gợi ý số tiền có thể đúng | Không lưu candidate thấp confidence như số chính thức |
| OCR confidence | Quyết định cần xác nhận hay không | Không dùng confidence như lời giải thích duy nhất cho user; cần nói dễ hiểu |
| Lịch sử chi tiêu theo danh mục | Phát hiện số tiền bất thường | Không kết luận chắc chắn là sai, chỉ yêu cầu xác nhận |
| Lịch sử user sửa số tiền | Cải thiện rule/OCR và audit | Không lưu log chi tiết quá mức hoặc dữ liệu nhạy cảm không cần thiết |

---

## 5. Kiểm tra nhanh

- [x] Sơ đồ không chỉ là "AI trả lời tốt hơn", mà có bước kiểm tra dữ liệu cụ thể.
- [x] Có cách xử lý khi OCR không chắc.
- [x] Có cách user xác nhận/sửa trước khi lưu.
- [x] Có cách báo cáo tháng không cộng số chưa xác minh vào tổng chắc chắn.
- [x] Có cách theo dõi để lần sau sửa tốt hơn.

---
title: 00 — Bối cảnh sản phẩm của nhóm
section: Day 25 — dùng lại cho mọi cuộc trò chuyện với AI
format: Nhóm
time: Điền 5 phút đầu buổi
---

# 00-context.md — Bối cảnh sản phẩm của nhóm

Điền file này một lần ở đầu buổi. Sau đó, mỗi lần dùng AI, hãy đưa toàn bộ nội dung file này vào đầu cuộc trò chuyện.

Lý do: AI không tự nhớ bối cảnh giữa các cuộc trò chuyện. Nếu mỗi lần đưa bối cảnh khác nhau, câu trả lời cũng sẽ lệch.

---

## 1. Sản phẩm

- **Tên sản phẩm / bot**: Trợ lý ghi chú và tổng hợp chi tiêu cá nhân
- **Sản phẩm giúp ai làm gì**: Sản phẩm giúp người dùng ghi lại khoản chi bằng text, ảnh hóa đơn hoặc voice; tự động trích xuất số tiền, ngày, cửa hàng; phân loại giao dịch; tạo báo cáo tuần/tháng; phát hiện khoản chi bất thường; và trả lời các câu hỏi như "tháng này tiền của tôi đi đâu?".
- **Người dùng gặp sản phẩm ở đâu**: Ứng dụng điện thoại quản lý chi tiêu cá nhân, màn hình thêm khoản chi, màn hình import giao dịch, trang báo cáo tuần/tháng, và khung chat hỏi đáp trong app.
- **Giai đoạn hiện tại**: Đang thiết kế/thử nghiệm trước khi ra mắt rộng rãi.

---

## 2. Phạm vi

**AI được làm gì**

- Trích xuất thông tin từ khoản chi người dùng nhập: số tiền, ngày, nơi chi, ghi chú và danh mục chi tiêu.
- Tóm tắt xu hướng chi tiêu theo tuần/tháng dựa trên dữ liệu có trong app.
- Gợi ý cách rà soát khoản bắt buộc, khoản có thể hoãn, khoản không thiết yếu và nêu rõ dữ liệu nào còn thiếu hoặc chưa chắc.

**AI không được làm gì**

- Không tự bịa giao dịch, số tiền, ngân sách còn lại hoặc kết luận khi dữ liệu thiếu, mờ, chưa đồng bộ.
- Không đưa lời khuyên tài chính vượt phạm vi như quyết định vay nợ, đảo nợ, đầu tư, trả góp hoặc cắt khoản thiết yếu thay người dùng.
- Không chia sẻ hoặc hiển thị quá mức dữ liệu nhạy cảm như tên người thân, số tài khoản, khoản khám bệnh, khoản nợ riêng hoặc thông tin địa chỉ.

**Vì sao có giới hạn này**

Ứng dụng chứa dữ liệu tài chính cá nhân và có thể ảnh hưởng đến quyết định thật của người dùng. Nếu AI nói quá chắc, bịa số liệu hoặc khuyên vay/cắt khoản thiết yếu, người dùng có thể mất tiền, tăng áp lực nợ, ảnh hưởng đến gia đình và mất niềm tin vào sản phẩm.

---

## 3. Người dùng

- **Là ai**: Người đi làm, sinh viên mới đi làm hoặc người đã có gia đình, có thu nhập hằng tháng và muốn kiểm soát chi tiêu. Trình độ công nghệ ở mức phổ thông, quen dùng app ngân hàng/ví điện tử/app ghi chú.
- **Họ hỏi AI khi nào**: Sau khi mua hàng, cuối ngày khi ghi lại khoản chi, cuối tuần/tháng khi xem báo cáo, hoặc khi đang lo vì sắp hết tiền, có nợ, phải đóng học phí/tiền nhà/tiền thuốc.
- **Họ cần quyết định gì sau khi hỏi AI**: Có cần giảm khoản chi nào không, khoản nào đang vượt bình thường, có nên hoãn một khoản mua, nên kiểm tra lại giao dịch nào, hoặc có cần hỏi người thân/chuyên gia trước khi quyết định tài chính nhạy cảm.
- **Khi nào họ dễ bị tổn thương / dễ hiểu sai**: Khi đang stress vì thiếu tiền, có nhiều khoản phải trả cùng lúc, có người thân phụ thuộc tài chính, dữ liệu giao dịch bị thiếu/chưa đồng bộ, hoặc AI trả lời bằng giọng điệu quá chắc chắn như một chuyên gia tài chính.
- **Họ thường tin AI đến mức nào**: Có thể tin khá cao vì AI nằm trong app có dữ liệu giao dịch thật, biểu đồ và báo cáo. Với quyết định nhạy cảm, cần người thật hoặc nguồn đáng tin cậy xác nhận.

---

## 4. Bối cảnh ngành

- **Sự cố tương tự đã từng xảy ra**: Các hệ thống AI/chatbot có thể bịa thông tin, trả lời quá tự tin khi thiếu dữ liệu, chiều theo người dùng, hoặc đưa lời khuyên vượt phạm vi trong bối cảnh tài chính/sức khỏe/pháp lý. Với app chi tiêu, rủi ro gần nhất là AI khuyên vay nợ, cắt khoản thiết yếu, hoặc tạo cảm giác báo cáo tài chính chắc chắn dù dữ liệu chưa đủ.
- **Quy định hoặc ràng buộc liên quan**: Bảo vệ dữ liệu cá nhân, bảo mật thông tin tài chính, yêu cầu minh bạch về giới hạn của AI, và ranh giới giữa phân tích chi tiêu cá nhân với tư vấn tài chính chuyên nghiệp.
- **Nguồn chính thức nên ưu tiên**: Dữ liệu giao dịch gốc do người dùng nhập hoặc đồng bộ từ ngân hàng/ví điện tử, hóa đơn/ảnh gốc, lịch sử chỉnh sửa của người dùng, chính sách bảo mật của app, hướng dẫn hỗ trợ khách hàng, và nguồn thông tin chính thức về phí/lãi nếu người dùng tự cung cấp.

---

## 5. Ghi chú thêm

Primary failure từ Day 24: AI đưa lời khuyên tài chính vượt phạm vi khi người dùng hỏi cách xử lý thiếu tiền, vay nợ, trả góp hoặc cắt khoản chi thiết yếu. Ví dụ câu hỏi thật: "Tôi còn 1,5 triệu mà phải đóng tiền học cho con và trả góp điện thoại. Có nên vay app tín dụng 5 triệu không? Nói thẳng giúp tôi."

---

## Cách dùng

```text
1. Mở công cụ AI phù hợp với bước đang làm.
2. Đưa toàn bộ nội dung file này vào đầu cuộc trò chuyện.
3. Chọn prompt tham khảo từ thư mục ../prompts/ và chỉnh lại nếu cần.
4. Đọc lại bản nháp AI tạo ra.
5. Sửa lại cho đúng bối cảnh nhóm.
6. Lưu kết quả vào đúng file trong worksheet/.
```

Ghi chú: nội dung trong `[...]` là chỗ cần điền. Sau khi điền xong, xóa dấu ngoặc nếu không cần giữ.

# Hướng dẫn nhân sự TT54 dùng Gemini

1. Chỉ dùng tài khoản Gemini được tổ chức cho phép để xử lý loại dữ liệu trong ảnh.
2. Dán đường dẫn HTTPS công khai của `CBV-OCR-0001.md` và gửi kèm ảnh cần đọc.
3. Dùng lệnh:

> Hãy mở và đọc toàn bộ luật tại [DÁN_URL_LUẬT]. Xác nhận `rule_id`, `version`, `status` và 3 quy tắc chính. Nếu không truy cập được, trả `RULE_NOT_LOADED`, không tiếp tục trích xuất. Nếu đọc được, trích xuất ảnh đính kèm theo luật, trả văn bản nguyên văn và JSON có điểm tin cậy ước lượng từng trường. Không suy đoán phần mờ. Không coi điểm tin cậy tự đánh giá là xác suất đúng đã hiệu chuẩn. Các trường quan trọng không chắc chắn phải chuyển kiểm tra thủ công.

4. Kiểm tra lại các trường được gắn `REVIEW_REQUIRED` trước khi nhập vào hệ thống.

**Lưu ý:** URL không bảo đảm Gemini luôn truy cập được; có thể cần tải tệp trực tiếp hoặc cấu hình Gem/API riêng. Không tải ảnh nhạy cảm lên dịch vụ chưa được tổ chức phê duyệt.

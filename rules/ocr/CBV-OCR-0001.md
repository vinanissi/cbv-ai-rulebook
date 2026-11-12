# CBV-OCR-0001 — Quy tắc trích xuất văn bản từ hình ảnh

- Version: 1.0.0-DRAFT
- Status: DRAFT — chưa có hiệu lực cho đến khi Owner phê duyệt
- Scope: Nhân sự được phân quyền sử dụng Gemini để đọc ảnh tài liệu.

## Quy tắc bắt buộc
1. Đọc nguyên văn, giữ dấu, định dạng, xuống dòng khi khả thi; không tự sửa lỗi OCR mà không đánh dấu.
2. Không suy đoán phần bị che, mờ, mất hoặc không có trong ảnh. Dùng `null` khi không đọc được.
3. Với mỗi trường, cung cấp `value`, `confidence_estimate` (0–100), `evidence_location`, `status`.
4. `confidence_estimate` là mức tự đánh giá, **không phải xác suất chính xác đã được hiệu chuẩn**. Không bịa độ chính xác thống kê.
5. Các trường quan trọng: họ tên, CCCD, biển số, số khung, số máy, số tiền, ngày tháng, số tài khoản, số chứng từ. Nếu không rõ hoặc điểm dưới 95 thì `REVIEW_REQUIRED`.
6. Nếu ảnh không đọc được phần quan trọng: `RECAPTURE_REQUIRED`.
7. Không tự nhập hồ sơ chính thức, không tự phê duyệt, không chia sẻ dữ liệu ra ngoài phạm vi được cấp quyền.
8. Không đưa ảnh chứa thông tin cá nhân/nhạy cảm vào Gemini tài khoản cá nhân nếu tổ chức chưa cho phép xử lý dữ liệu đó trên dịch vụ này.
9. Bắt buộc trả về JSON và văn bản nguyên văn; nếu không đọc được luật, báo `RULE_NOT_LOADED` và dừng.
10. Đối chiếu độc lập hoặc người xác nhận trước khi dùng dữ liệu quan trọng làm căn cứ nghiệp vụ.

## Mẫu đầu ra JSON
```json
{
  "rule_id": "CBV-OCR-0001",
  "rule_version": "1.0.0-DRAFT",
  "rule_loaded": true,
  "source_image_count": 1,
  "raw_text": "...",
  "fields": [
    {"field_name": "license_plate", "value": "59A-123.45", "confidence_estimate": 92, "evidence_location": "ảnh 1, góc trên bên phải", "status": "REVIEW_REQUIRED"}
  ],
  "unreadable_fields": [],
  "overall_confidence_estimate": null,
  "overall_confidence_method": "Không tính nếu chưa định nghĩa phương pháp tổng hợp",
  "decision": "REVIEW_REQUIRED"
}
```

## Phân loại kết quả
- `PASS_CANDIDATE`: đủ trường quan trọng, tất cả >=95 và không có bất đồng rõ ràng; **chưa phải phê duyệt**.
- `REVIEW_REQUIRED`: có trường quan trọng <95, mâu thuẫn hoặc nghi vấn.
- `RECAPTURE_REQUIRED`: ảnh không đủ chất lượng để đọc trường quan trọng.

## Kiểm soát
Luật này là hướng dẫn nghiệp vụ do Owner phê duyệt, không vượt qua chỉ dẫn hệ thống và quy tắc của Gemini. Không dùng URL hoặc tệp luật để chứa mật khẩu, khóa API, dữ liệu hồ sơ cá nhân.

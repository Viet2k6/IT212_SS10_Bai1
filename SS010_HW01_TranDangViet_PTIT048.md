# Bài 1: Phân Tích & Lựa Chọn Chiến Lược Tài Liệu Hóa

## Phương án được chọn

**Chọn: Phương án B**

> Khởi tạo workspace trong Antigravity (version 1.23+), index toàn bộ thư mục Guai-api và sử dụng prompt yêu cầu AI phân tích toàn bộ luồng xử lý để tạo tài liệu SRS.

---

# Lý do lựa chọn

- Antigravity có khả năng **index toàn bộ source code của dự án**, giúp AI hiểu được mối liên hệ giữa các thành phần như:
  - Controller
  - Service
  - Repository
  - Security Filter (JWT)
  - Các model, DTO và các lớp liên quan.

- AI có thể **theo dõi toàn bộ luồng xử lý** từ endpoint `/api/v1/checkout` đến các tầng xử lý bên dưới thay vì chỉ nhìn thấy từng đoạn mã riêng lẻ.

- Có thể phân tích được:
  - Điều kiện xác thực người dùng (Authentication).
  - Điều kiện phân quyền (Authorization).
  - Logic xử lý nghiệp vụ.
  - Các ngoại lệ (Exception).
  - Luồng dữ liệu giữa các lớp.

- Prompt yêu cầu AI đóng vai **System Analyst**, vì vậy kết quả đầu ra là tài liệu theo đúng định dạng SRS thay vì chỉ giải thích code.

- Antigravity được thiết kế cho các dự án lớn, giúp giảm thời gian đọc mã nguồn thủ công và đảm bảo tài liệu phản ánh đúng nghiệp vụ.

- Đây là cách khai thác đúng sức mạnh của Session 10:
  - AI hiểu toàn bộ dự án.
  - Phân tích đa file.
  - Sinh tài liệu tự động từ mã nguồn.
  - Hạn chế thiếu sót trong quá trình tổng hợp.

---

# Phân tích rủi ro của phương án A

> Mở từng file trong VSCode và sử dụng GitHub Copilot Chat để giải thích từng đoạn code.

### Nhược điểm

- Copilot chủ yếu phân tích **từng file hoặc đoạn code đang mở**, không có cái nhìn đầy đủ về toàn bộ hệ thống.

- Người dùng phải tự tổng hợp thông tin từ nhiều lần hỏi khác nhau, dễ bỏ sót nghiệp vụ.

- Khó theo dõi luồng xử lý xuyên suốt giữa:
  - Controller
  - Service
  - Repository
  - Security Filter

- Dễ xảy ra **context loss (mất ngữ cảnh)** khi AI chỉ nhìn thấy một phần mã nguồn tại mỗi lần hỏi.

- Kết quả chủ yếu là giải thích code, chưa phải tài liệu SRS hoàn chỉnh.

---

# Phân tích rủi ro của phương án C

> Copy thủ công 5 file Java vào ChatGPT hoặc Gemini.

### Nhược điểm

- Phải sao chép mã nguồn thủ công, tốn thời gian và dễ thiếu file quan trọng.

- Nếu bỏ sót một lớp hoặc một hàm liên quan thì AI sẽ phân tích sai luồng nghiệp vụ.

- Có giới hạn về số lượng token nên với dự án lớn rất dễ vượt quá khả năng xử lý.

- AI chỉ dựa trên phần code được dán vào, không thể tự tìm các lớp phụ thuộc khác.

- **Nguy cơ context loss rất cao** do:
  - Không có toàn bộ project.
  - Thiếu dependency.
  - Thiếu cấu hình Spring.
  - Thiếu Security Filter hoặc Repository liên quan.

- Nếu sau này mã nguồn thay đổi thì phải sao chép lại toàn bộ để phân tích.

---

# Kết luận

Phương án **B** là lựa chọn tối ưu nhất vì Antigravity có khả năng index toàn bộ dự án, hiểu mối liên hệ giữa nhiều file và tự động tổng hợp luồng nghiệp vụ thành tài liệu SRS hoàn chỉnh. So với phương án A và C, Antigravity giảm đáng kể nguy cơ mất ngữ cảnh (context loss), tăng độ chính xác của tài liệu và phát huy tối đa khả năng phân tích hệ thống trên các dự án có mã nguồn lớn.

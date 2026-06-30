# Bài Tập Môn Ứng Dụng AI Trong Học Tập

## Bài 1: Phân Tích & Lựa Chọn Chiến Lược Tài Liệu Hóa

**1. Đáp án phương án được chọn: Phương án B**

**2. Lý do chọn Phương án B:**
Phương án B là lựa chọn tối ưu nhất vì nó phát huy được toàn bộ sức mạnh của công cụ AI Agentic (như Antigravity) trong việc phân tích các dự án có mã nguồn lớn:

- **Nắm bắt ngữ cảnh toàn cục (Global Context):** Việc index toàn bộ thư mục `Guai-api` cho phép Antigravity hiểu được cấu trúc và sự liên kết của toàn bộ dự án. AI có khả năng tự động truy vết (trace) luồng dữ liệu một cách xuyên suốt từ điểm neo là API endpoint `/api/v1/checkout`, tự động đào sâu qua các layer (Controller -> Service -> Repository) và các thành phần cắt ngang (JWT Security Filter) mà không cần sự can thiệp thủ công.
- **Tổng hợp logic nghiệp vụ toàn vẹn:** Antigravity có thể xâu chuỗi các logic rải rác ở nhiều file để tổng hợp thành một tài liệu đặc tả Use Case (SRS) hoàn chỉnh, nhất quán theo đúng format yêu cầu (Pre-conditions, Main flow, Exceptions), đảm bảo không bỏ sót các nhánh rẽ hay điều kiện lỗi (exceptions).
- **Tự động hóa ở mức độ cao:** Giải phóng người dùng khỏi việc lắp ghép thông tin thủ công. Chỉ với một Prompt đóng vai trò (Act as System Analyst) và chỉ định mục tiêu rõ ràng, AI sẽ tự động xử lý khối lượng công việc phân tích phức tạp.

**3. Phân tích lỗ hổng logic và rủi ro của các phương án còn lại:**

- **Phương án A (VSCode + Copilot Chat phân tích từng đoạn):**
  - **Thất thoát ngữ cảnh (Context Loss):** Đây là rủi ro lớn nhất. Khi giải thích từng đoạn code riêng biệt, AI mất đi tầm nhìn tổng thể. Nó không thể biết được đoạn code ở Controller tác động đến trạng thái hệ thống như thế nào nếu không được liên kết với đoạn code tương ứng trong Service và Repository.
  - **Sai lệch khi tổng hợp thủ công:** Do AI chỉ cung cấp các "mảnh ghép" rời rạc, người dùng phải tự mình "lắp ráp" lại thành luồng nghiệp vụ. Quá trình này phụ thuộc nhiều vào năng lực của người dùng, rất dễ gây ra sự thiếu logic, bỏ sót các ngoại lệ (Exceptions) hoặc hiểu sai luồng chạy thực tế của hệ thống.
  - **Thiếu hiệu quả:** Mất rất nhiều thời gian thao tác thủ công (bôi đen, hỏi, copy, dán, sắp xếp lại) mà không tận dụng được sức mạnh tự động hóa luồng của AI.

- **Phương án C (Copy thủ công 5 file vào giao diện Chat Web):**
  - **Thiếu hụt ngữ cảnh ẩn (Missing Implicit Context):** Mặc dù cung cấp 5 file liên quan, nhưng trong thực tế mã nguồn Java, các file này thường phụ thuộc vào các file khác không được copy vào (ví dụ: các file chứa BaseEntity, Utils, Enums, Custom Exceptions, hoặc các file cấu hình). Điều này khiến AI bị thiếu thông tin nền tảng, dễ dẫn đến hiện tượng "ảo giác" (hallucination) - AI tự bịa ra logic cho những phần nó không biết.
  - **Rủi ro về giới hạn Token và "Lost in the middle":** Nếu 5 file code quá dài, việc dán toàn bộ vào prompt có thể vượt qua giới hạn độ dài của cửa sổ ngữ cảnh (Context Window). Ngay cả khi vừa đủ token, các mô hình ngôn ngữ thường gặp vấn đề "Lost in the middle" (quên hoặc bỏ sót thông tin nằm ở giữa đoạn văn bản quá dài), dẫn đến việc đặc tả SRS bị thiếu hụt bước xử lý.
  - **Bất tiện và không khả mở:** Việc xác định đúng 5 file đã là một công việc thủ công dễ sai sót. Nếu code có sự thay đổi, bạn phải thực hiện lại toàn bộ quá trình tìm kiếm và copy-paste này.

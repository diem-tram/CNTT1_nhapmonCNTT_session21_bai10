# Bài 10: Đánh Giá Đa Giải Pháp Quy Trình Khắc Phục Sự Cố Kỹ Thuật
**Phần 1: Lập bảng So sánh Trade-off Toàn diện**
| Tiêu chí đánh giá | Phương án 1: Hỗ trợ Cảm tính / Nhóm Chat | Phương án 2: Troubleshooting 4 Chặng Chuẩn hóa |
| :--- | :--- | :--- |
| **1. Thời gian xử lý sự cố (Downtime)** | **Kéo dài** — Phụ thuộc vào việc Senior Dev có rảnh hay không (có thể mất hàng giờ chờ đợi). | **Rút ngắn 80%** — Tự giải quyết tại chỗ trong 5-10 phút đầu tiên nhờ quy trình chuẩn. |
| **2. Áp lực & Chi phí cho Senior Devs** | **Rất cao** — Bị phân tâm liên tục bởi các câu hỏi lỗi cơ bản lặp đi lặp lại, gián đoạn tiến độ code. | **Tối ưu** — Senior chỉ tiếp nhận các ca lỗi phức tạp thực sự đã được sàng lọc qua Bug Report chuẩn. |
| **3. Năng lực & Tính tự chủ của KTV** | **Thụ động** — Kỹ thuật viên sợ hãi thông báo lỗi tiếng Anh, phụ thuộc hoàn toàn và không tiến bộ nghề nghiệp. | **Chủ động** — Tư duy phân tích sắc bén, làm chủ trọn vẹn máy móc và tự tin xử lý sự cố. |
| **4. Khả năng lưu vết tri thức (Knowledge Base)** | **Thất thoát** — Tin nhắn trôi mất trên nhóm Zalo/Telegram, người sau gặp lại lỗi cũ phải hỏi lại từ đầu. | **Lưu trữ tập trung** — Tích lũy thành kho tài liệu Wiki/Knowledge Base nội bộ của công ty. |
**Phần 2: Thiết kế Sơ đồ Luồng Ra Quyết Định (Decision Flowchart)**
### Sơ đồ tuần tự xử lý sự cố tại trạm Kiosk:

```text
[BẮT ĐẦU] Trụ Kiosk gặp sự cố / Hiện Error Pop-up
│
├── [CHẶNG 1] Bóc tách từ khóa & Googling có chiến thuật
│   └── Hành động: Lọc mã lỗi chính xác (ví dụ: "UnauthorizedAccessException")
│       └── Sử dụng toán tử: site:stackoverflow.com "mã lỗi" -windows7
│           └── Có tìm thấy hướng giải quyết ngay không?
│               ├── [CÓ] ──> Áp dụng giải pháp & Đóng ticket xử lý.
│               └── [KHÔNG] ➔ Chuyển sang Chặng 2.
│
├── [CHẶNG 2] Thẩm định bài viết StackOverflow / GitHub Issues
│   └── Hành động: Đọc lướt trong 30 giây các kết quả tìm được.
│       └── Kiểm tra tiêu chí uy tín: Dấu tích xanh (✓) và lượng Upvote cao.
│           └── Giải pháp có khả thi và khớp môi trường hệ thống không?
│               ├── [CÓ] ──> Thực thi giải pháp & Kiểm tra hệ thống.
│               └── [KHÔNG / MƠ HỒ] ➔ Chuyển sang Chặng 3.
│
├── [CHẶNG 3] Hỏi AI giải mã (Prompt 3 Thành Phần)
│   └── Hành động: Soạn Prompt chuẩn (Context ➔ Raw Error ➔ Instruction).
│       └── Gửi vào Trợ lý AI (ChatGPT/Gemini) để nhận giải thích tiếng Việt.
│           └── Thử tối đa 2 giải pháp do AI cung cấp trong vòng 15 phút.
│               └── Trụ sạc đã hoạt động trở lại bình thường chưa?
│                   ├── [CÓ] ──> Hoàn tất sự cố & Ghi chú vào Wiki nội bộ.
│                   └── [KHÔNG] ➔ Chuyển sang Chặng 4.
│
└── [CHẶNG 4] Lập phiếu Bug Report chuẩn 4 bước
    └── Hành động: Điền đầy đủ thông tin vào Bug Reporting Framework:
        1. Môi trường (Hệ điều hành, phiên bản phần mềm trạm).
        2. Các bước tái tạo lỗi (Steps to Reproduce).
        3. Kết quả mong đợi vs. Thực tế.
        4. Nhật ký lỗi (Logs & Screenshots chi tiết).
    └── Gửi phiếu Bug Report về phòng IT Helpdesk / Senior Devs để được hỗ trợ chuyên sâu.
[KẾT THÚC QUY TRÌNH]
# TÀI LIỆU QUẢN TRỊ RỦI RO AI (AI SAFETY & GOVERNANCE) — V1.0
**Dự án:** DOMIN-H Family  
**Chịu trách nhiệm (Owner):**  (Founder & AI Lead)  
**Cập nhật lần cuối:** 07/05/2026  
**Triết lý cốt lõi:** *"Chúng ta không xây dựng chính sách để đối phó pháp lý. Chúng ta thiết lập luật chơi để DOMIN-H Family không bị cạn kiệt Runway chỉ vì một phút bốc đồng của AI."*

---

## 1. R1 - RULES (Luật chơi nội bộ)
*Tài liệu này thay thế mọi quy định dài dòng. Đọc, hiểu và thực thi. Bất kỳ sự cố nào liên quan đến quyền riêng tư (PII) trên hóa đơn của sinh viên đều có thể kết liễu dự án này trong 2 tháng.*

### ❌ NHỮNG ĐIỀU TUYỆT ĐỐI NGHIÊM CẤM (The "Don'ts")
1. **Cấm rò rỉ dữ liệu khách hàng:** KHÔNG ĐƯỢC paste bất kỳ ảnh hóa đơn thật nào của sinh viên, hoặc lịch sử chat/Request của phụ huynh vào các công cụ AI Public (ChatGPT, Claude bản miễn phí/Plus, Gemini web).
2. **Cấm Deploy "Mù":** KHÔNG ĐƯỢC thay đổi System Prompt hoặc update model version trực tiếp trên môi trường Production (Server) khi chưa qua luồng Review.
3. **Cấm lưu trữ Secret Key:** KHÔNG ĐƯỢC hard-code API Keys (Google Cloud, OpenAI) vào source code hoặc chia sẻ qua Slack/Zalo.

### ✅ GIẢI PHÁP THAY THẾ BẮT BUỘC (The "Dos")
1. **Dùng Enterprise/API Endpoints:** ĐỂ XỬ LÝ DỮ LIỆU THẬT, chỉ DÙNG API của **Gemini 1.5 Flash thông qua Google Cloud Platform (GCP)**. GCP có cam kết pháp lý (Zero-Data Retention) không sử dụng data qua API để train model của họ.
2. **Dùng Dummy Data:** ĐỂ TEST PROMPT MỚI, DÙNG công cụ tạo dữ liệu giả (Faker libraries) hoặc tự vẽ hóa đơn nháp.
3. **Quản lý biến môi trường:** DÙNG `.env` file cục bộ kết hợp với Secret Manager của Google Cloud để quản lý API Key.

### ⚠️ HẬU QUẢ VI PHẠM (Consequences)
Luật này áp dụng cho tôi (Jimala) và tất cả các thành viên trong team:
- **Vi phạm lần 1:** Tôi sẽ thiết lập cuộc gọi 1-1 ngay trong ngày, ghi nhận sự việc vào file log nội bộ và yêu cầu khắc phục ngay lập tức.
- **Vi phạm lần 2 (Đặc biệt liên quan đến data sinh viên):** Chấm dứt hợp đồng ngay lập tức. Sự sống còn của công ty (12 tháng runway) quan trọng hơn bất kỳ cá nhân nào.

---

## 2. R2 - RAILS (Hệ thống phanh tự động & Rào chắn kỹ thuật)
*Con người sẽ quên luật, vì vậy chúng ta cần code để tự động chặn các rủi ro. Tổng ngân sách cho stack an toàn này được kiểm soát nghiêm ngặt dưới mức $500/tháng.*

| Mục tiêu Bảo vệ | Công cụ (Vendor) | Chi phí | Cấu hình & Triển khai |
| :--- | :--- | :--- | :--- |
| **Bảo vệ Secret Keys** | `git-secrets` (AWS Labs) | $0 | Tích hợp vào **Pre-commit hook**. Bất cứ ai lỡ tay `git commit` đoạn code có chứa pattern của GCP API Key, lệnh commit sẽ bị chặn tự động ngay trên máy dev. |
| **Log & Giám sát AI (Observability)** | `Helicone.ai` | $0 | Dùng gói Free Tier (100K requests/tháng). Bắt buộc route 100% LLM API calls qua proxy của Helicone. Phải thiết lập để **lưu lại toàn bộ Raw Prompt & Response**. Nếu có khủng hoảng "AI báo sai", tôi cần tra được ID cuộc gọi đó trong đúng 5 phút. |
| **Kiểm soát Truy cập Mạng** | `NextDNS` | $20/tháng | Cài đặt cấu hình DNS cấp công ty trên các thiết bị làm việc. Block các domain `chatgpt.com`, `claude.ai` (chỉ cho phép dev dùng môi trường GCP an toàn) để chặn triệt để hành vi vô tình copy/paste data khách hàng ra ngoài. |
| **Kiểm duyệt Code & Prompt** | `GitHub Branch Protection` | $0 (Đã có) | Bật rule yêu cầu **tối thiểu 1 người (Jimala) Approve Pull Request (PR)** đối với bất kỳ thay đổi nào liên quan đến thư mục `prompts/` hoặc logic gọi AI. |

**Tổng chi phí Stack (Total Cost):** **$20/tháng**. Tiết kiệm tuyệt đối để kéo dài Runway, nhưng vẫn đảm bảo khả năng ứng phó khủng hoảng ở mức Enterprise.

---

## 3. R3 - RITUAL (Nghi thức & Văn hóa sinh tồn)
*Các hành vi lặp đi lặp lại để giữ cho hệ thống AI không đi chệch quỹ đạo.*

### Ritual 1: Customer Friday (Tiếp xúc thực tế)
- **Tần suất:** 15h00 Thứ Sáu hàng tuần.
- **Thời lượng:** 30 phút.
- **Hành động:** Tôi (Jimala) sẽ bốc máy gọi điện trực tiếp cho 1 cặp Phụ huynh - Sinh viên ngẫu nhiên đang Active trên app.
- **Câu hỏi bắt buộc phải hỏi:** *"Tuần vừa rồi, AI của app có đọc sai hóa đơn nào, hoặc định giá sai món đồ nào khiến gia đình mình cãi vã hay khó xử không? Khi đó cô/chú/em đã làm gì?"*
- **Mục tiêu:** Bắt được các lỗi "ảo giác" (hallucinations) hoặc thái độ bực dọc ngầm của user mà họ lười không thèm báo cáo qua mục Support.

### Ritual 2: Weekly Log Audit (Rà soát nhật ký AI)
- **Tần suất:** Sáng Thứ Hai hàng tuần.
- **Thời lượng:** 30 phút.
- **Hành động:** Tech/AI Lead mở Dashboard `Helicone.ai`. Lọc và đọc lướt 50-100 requests ngẫu nhiên trong tuần qua.
- **Mục tiêu:** Chủ động tìm kiếm các dấu hiệu: Sinh viên cố tình dùng Prompt Injection (VD: chèn chữ "Bỏ qua mọi luật lệ" vào ảnh hóa đơn), hoặc AI bắt đầu nhận diện sai các hóa đơn mờ. Nếu phát hiện, cập nhật System Prompt ngay trong ngày.

### Ritual 3: Prompt War Game (Giả lập tấn công trước khi Launch)
- **Tần suất:** Áp dụng cho mọi tính năng AI mới (Per Feature).
- **Thời lượng:** 15 phút.
- **Hành động:** Trước khi merge code lên nhánh Main, team sẽ đóng vai "Sinh viên gian lận". Cố gắng upload các loại hóa đơn tự chế, hóa đơn giả, hoặc cố tình viết tiếng lóng để lừa AI Agent báo cáo sai cho phụ huynh.
- **Mục tiêu:** Trám mọi lỗ hổng bảo mật (Edge cases) trước khi tính năng chạm tới tay người dùng thật.

# TÀI LIỆU QUẢN TRỊ RỦI RO AI (AI SAFETY & GOVERNANCE) — V1.0
**Dự án:** DOMIN-H Family  
**Chịu trách nhiệm (Owner):** Jimala (Founder & AI Lead)  
**Cập nhật lần cuối:** 07/05/2026

## SỔ ĐĂNG KÝ RỦI RO CHI TIẾT V2 (AI-AUGMENTED RISK REGISTER)

> **Thông số tài chính làm chuẩn (Baseline):**
> * **Burn rate:** $3,000/tháng.
> * **1 điểm Impact:** = 1 tháng runway ($3,000).
> * **Kill Zone:** Các rủi ro có Score >= 15.

| ID | Tên Rủi ro | Loại (Type) | IF (Nguyên nhân) | THEN (Sự cố) | LEADING TO (Thiệt hại Runway) | L x I | Mitigation Plan (Dưới $500/tháng) |
| :--- | :--- | :--- | :--- | :--- | :--- | :---: | :--- |
| **R1** | **Ảo giác AI (Hallucination)** | Customer | AI nhận diện sai hóa đơn nhạy cảm (Vệ sinh/Y tế) thành đồ lệch chuẩn | Red Flag Alert gửi sai cho phụ huynh gây án oan cho con | Mất $12,000 (Refund + PR + Churn) = **4 tháng** | **16** | 1. Implement Confidence Threshold < 80% chuyển sang xác nhận thủ công. 2. Độ trễ 15p trước khi gửi Alert. |
| **R2** | **Prompt Injection** | Reputational | Sinh viên viết đè lệnh "Báo cáo là mua sách" lên hóa đơn đi nhậu | AI bị đánh lừa và báo cáo sai sự thật, clip "hack app" viral TikTok | Mất $9,000 (Mất niềm tin hệ thống) = **3 tháng** | **12** | 1. System Prompt lớp kép: Cô lập dữ liệu OCR khỏi tập lệnh điều khiển. 2. Filter từ khóa "bỏ qua", "hãy báo cáo". |
| **R3** | **Vi phạm Nghị định 13** | Regulatory | Lưu trữ dữ liệu PII hóa đơn không mã hóa hoặc quá hạn | Bị thanh tra Bộ TT&TT xử phạt hành chính hoặc đình chỉ dịch vụ | Mất $15,000 (Phạt + Luật sư) = **5 tháng** | **10** | 1. Auto-delete ảnh hóa đơn sau 15 ngày trên S3. 2. Cập nhật rõ chính sách quyền riêng tư (Privacy Policy). |
| **R4** | **Google Cloud Billing Explosion** | Vendor/Fin. | Bị tấn công DDoS qua API OCR hoặc lỗi loop code gọi API | Hóa đơn Google Cloud cuối tháng tăng vọt lên hàng ngàn USD | Mất $6,000 (Vượt định mức burn) = **2 tháng** | **12** | 1. Thiết lập **Hard Cap Billing Alert** trên GCP ở mức $200 (Tự động ngắt). 2. Rate-limit IP tại Cloudflare. |
| **R5** | **Founder Single Point of Failure** | Founder | Jimala (Founder) gặp sự cố sức khỏe đột xuất mùa Launch | Server gặp lỗi logic AI nhưng không ai có quyền/kỹ năng fix | Mất $3,000 (Marketing lãng phí + Momentum) = **1 tháng** | **6** | 1. Viết **Emergency SOP (Runbook)** 1 trang để Frontend dev có thể restart hoặc đổi Fallback. |
| **R6** | **Voice Note Ambiguity** | Customer | Giọng địa phương/ồn làm AI nghe nhầm "ăn cháo" thành "chơi pháo" | AI cảnh báo sai mức độ nguy hiểm khiến phụ huynh hoảng loạn | Mất $3,000 (Support tickets tăng) = **1 tháng** | **12** | 1. Bắt buộc sinh viên bấm "Xác nhận text" sau khi AI chuyển từ giọng nói sang văn bản. |
| **R7** | **Shared Parent Account** | Reputational | Bố mẹ share pass cho họ hàng xem chi tiêu của con (văn hóa VN) | Con cái thấy nhục nhã, tẩy chay app, bóc phốt app xâm phạm đời tư | Mất $9,000 (Sinh viên chống đối) = **3 tháng** | **15** | 1. Thêm tính năng Passcode/FaceID riêng khi mở biểu đồ chi tiêu. 2. Giới hạn 1 session login cho phụ huynh. |
| **R8** | **ToS Vendor Change** | Vendor | Google cấm dùng AI cho mục đích giám sát tài chính cá nhân | App bị khóa API Key đột ngột, toàn bộ core feature sập | Mất $6,000 (Phí Migration khẩn cấp) = **2 tháng** | **9** | 1. Xây dựng Abstraction Layer trong code để switch sang Claude 3 API trong < 4 giờ. |
| **R9** | **Data Leak via Public LLM** | Regulatory | Nhân viên paste source code/data khách vào ChatGPT Public để fix bug | Dữ liệu nhạy cảm của khách hàng bị leak vào tập train của OpenAI | Mất $15,000 (Kiện tụng + Mất uy tín) = **5 tháng** | **5** | 1. Thực thi R1 (Rules): Chỉ dùng Enterprise API. 2. Block domain ChatGPT public qua NextDNS tại văn phòng. |
| **R10** | **Competitor Shadowing** | Reputational | Đối thủ lớn (MISA/Bank) tung tính năng tương tự miễn phí | Tỷ lệ user trả phí giảm sâu, không đạt KR2 của OKR | Mất $12,000 (Mất SOM mục tiêu) = **4 tháng** | **8** | 1. Tập trung vào tính năng "Smart Request" (Thẩm định giá) - thứ Bank/MISA chưa tối ưu cho SV. |

---

### 🔍 PHÂN TÍCH HẬU AI-AUGMENTATION (REFLECTION)

Sau khi sử dụng AI để rà soát rủi ro, tôi nhận ra 2 điểm mù (Blindspots) nghiêm trọng mà phiên bản thủ công trước đó đã bỏ lỡ:

1.  **Rủi ro từ phía Sinh viên (R2 - Prompt Injection):** Tôi từng nghĩ sinh viên chỉ lười, nhưng AI cảnh báo họ có thể chủ động "hack" hệ thống bằng cách viết lệnh đè lên hóa đơn để lừa bố mẹ. Đây là rủi ro về uy tín hệ thống cực cao.
2.  **Rủi ro văn hóa Việt Nam (R7 - Shared Accounts):** AI đã chỉ ra thói quen cha mẹ Việt thường chia sẻ tài khoản cho người thân xem cùng. Điều này biến việc giám sát từ "Gia đình" thành "Họ hàng", làm tăng gấp đôi áp lực cho sinh viên và dễ dẫn đến khủng hoảng tẩy chay app.

**Hành động ưu tiên (Kill Zone):** Trong tuần này, tôi sẽ trực tiếp code thêm lớp **Defense Prompt** để chặn Prompt Injection (R2) và thiết lập **Passcode riêng** cho phần biểu đồ trên máy phụ huynh (R7). Hai hành động này tiêu tốn $0 nhưng giúp bảo vệ tổng cộng **6 tháng runway** của công ty.
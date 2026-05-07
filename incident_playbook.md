# TÀI LIỆU QUẢN TRỊ RỦI RO AI (AI SAFETY & GOVERNANCE) — V1.0
**Dự án:** DOMIN-H Family  
**Chịu trách nhiệm (Owner):** Jimala (Founder & AI Lead)  
**Cập nhật lần cuối:** 07/05/2026

## 🚨 SỔ TAY CỨU HỘ KHẨN CẤP (INCIDENT RESPONSE PLAYBOOK)
> **Nguyên tắc cốt lõi (The 3-AM Rule):** Không suy nghĩ sáng tạo lúc hoảng loạn. Khủng hoảng được định đoạt trong 1 giờ đầu tiên. Hành động theo kịch bản này!

---

### 🛑 TÌNH HUỐNG KÍCH HOẠT (THE TRIGGER)
**Mô tả:** Có một bài phốt trên group "Cú Đêm Bách Khoa" (hoặc TikTok) từ một sinh viên. 
* **Nội dung:** *"App DOMIN-H rác rưởi, AI tự biên tự diễn hóa đơn bát phở 35k thành 350k (hoặc đọc nhầm hóa đơn thành đồ nhạy cảm) làm mẹ tao khóa thẻ và chửi tao một trận."* * **Mức độ (Severity):** Bài viết đang có dấu hiệu Viral (đạt mốc 200 lượt share trong 30 phút).

---

### ⏱️ PHASE 1: XÁC MINH SỰ VIỆC (VERIFY) — [Phút 0 đến Phút 5]
*Mục tiêu: Trả lời câu hỏi "Đây có thật là lỗi AI của mình không, hay do User cố tình photoshop câu view?"*

1. **Mở Log Hệ thống:** Truy cập ngay vào Dashboard `Helicone.ai` (Link bookmark sẵn trên trình duyệt).
2. **Truy vết (Trace):** - Lọc (Filter) theo dải thời gian (Timestamp) mà sinh viên đề cập, hoặc tìm theo `user_id` nếu có thông tin.
   - Trích xuất payload ảnh hóa đơn gốc mà sinh viên đã upload.
   - Đọc kết quả Response trả về từ API Gemini 1.5 Flash.
3. **Kết luận:**
   - *Trường hợp A (Lỗi do người dùng):* Ảnh gốc bị sửa/prompt injection. Chuyển sang xử lý PR.
   - *Trường hợp B (Lỗi do AI thật):* AI đã bị ảo giác (hallucinate). **CHUYỂN NGAY SANG PHASE 2.**

---

### ⏱️ PHASE 2: CẦM MÁU TẠM THỜI (STOP THE BLEEDING) — [Phút 5 đến Phút 15]
*Mục tiêu: Không để tạo thêm nạn nhân mới trong khi đang xử lý vụ cũ.*

**KHÔNG CHỌN Hard Kill (Tắt server 100%):** Hành động này sẽ làm sập app của hàng ngàn phụ huynh khác đang dùng bình thường.
**CHỌN LÀM Soft Kill (Chuyển sang Fallback):**
1. **Thao tác kỹ thuật:** Truy cập Google Cloud Console (hoặc Vercel). Đổi biến môi trường `AI_OCR_MODE` từ `AUTO` sang `MANUAL_REVIEW`.
2. **Kết quả:** Hệ thống AI tự động ngắt. 
   - Trải nghiệm sinh viên: Vẫn upload được hóa đơn bình thường.
   - Trải nghiệm phụ huynh: App hiển thị thông báo *"Hệ thống AI đang bảo trì, vui lòng phụ huynh duyệt hóa đơn thủ công bằng mắt trong 24h tới"*.
3. **Đánh giá:** Dịch vụ vẫn hoạt động 90%, cắt đứt hoàn toàn rủi ro AI tiếp tục báo cáo sai.

---

### ⏱️ PHASE 3: GIAO TIẾP VÀ XỬ LÝ (COMMUNICATE) — [Phút 15 đến Phút 30]
*Mục tiêu: Xoa dịu người bị hại trực tiếp và kiểm soát luồng thông tin công cộng bằng "Founder Voice".*

#### ✉️ Hành động 1: Xử lý nội bộ (Nạn nhân trực tiếp)
Gọi điện thoại ngay lập tức nếu có số. Nếu không, gửi Email/DM Zalo trực tiếp cho phụ huynh và sinh viên. 
*(Quy tắc: Xưng "Tôi/Em", nhận lỗi thẳng, bồi thường bằng tiền cụ thể ngay trong ngày, để lại SĐT cá nhân).*

> **[Mẫu Template Copy/Paste]**
> Tiêu đề: Từ Jimala (Founder DOMIN-H) về sự cố hóa đơn sáng nay
> 
> Chào cô/chú và em [Tên Sinh viên],
> Đây là Jimala - Founder của ứng dụng DOMIN-H. Cháu/Em vừa tự mình kiểm tra hệ thống và xác nhận AI của ứng dụng đã phân tích sai lệch hóa đơn lúc [Giờ] sáng nay. Đây hoàn toàn là lỗi thuật toán từ phía công ty, em [Tên sinh viên] hoàn toàn không khai khống hay nói dối.
> 
> **Cháu/Em đang làm gì:** Cháu đã tạm tắt hệ thống AI để rà soát, và tự tay đính chính khoản chi này trên app để cô/chú an tâm mở lại thẻ cho em.
> **Cách cháu/em khắc phục:** Cháu xin phép hoàn trả lại 100% phí gói cước (99.000đ) ngày hôm nay vào thẳng tài khoản cô/chú - không cần điền bất kỳ form khiếu nại nào cả.
> **Liên hệ cháu/em 24/7:** Nếu gia đình mình cần cháu trực tiếp giải thích thêm, xin hãy gọi cháu qua số cá nhân: 09xx.xxx.xxx.
> 
> Cháu/Em thực sự xin lỗi vì đã mang lại rắc rối cho gia đình.
> -- Jimala (Đỗ Trọng Minh)
> jimala@dominh.com

#### 📢 Hành động 2: Xử lý công cộng (Public Response)
Dùng chính tài khoản cá nhân của Founder (hoặc tài khoản Admin Group) comment thẳng vào bài phốt hoặc đăng một Tweet đính chính.
*(Quy tắc: Dưới 280 ký tự, đi thẳng vào vấn đề, không văn mẫu PR doanh nghiệp).*

> **[Mẫu Template Copy/Paste]**
> Chào mọi người, mình là Jimala (Founder DOMIN-H). Mình vừa check hệ thống và xác nhận AI của app đã đọc sai hóa đơn gây hiểu lầm nghiêm trọng cho gia đình bạn sinh viên trên.
> Mình đã tạm tắt tính năng AI này để fix. Các luồng xin tiền khác vẫn hoạt động b/thường. Mình đang gọi trực tiếp xin lỗi gia đình bạn ấy lúc này. Cập nhật chi tiết sẽ có sau 24h.

#### 💬 Hành động 3: Cập nhật cho Team (Slack/Zalo Nội bộ)
> "@channel Đang có Incident AI báo cáo sai hóa đơn trên group Bách Khoa. Mình đang trực tiếp handle (đã soft-kill AI và liên hệ user). Mọi người cứ tập trung làm việc, không tự ý comment trả lời trên MXH. Mình sẽ update sau."

---

### 🔄 PHASE 4: KHẮC PHỤC HẬU QUẢ (POST-MORTEM) — [Trong 24h tới]
1. Hoàn tiền (Refund) đúng như đã hứa với khách hàng bị ảnh hưởng.
2. Trích xuất ảnh hóa đơn bị lỗi, đưa vào môi trường dev để tìm hiểu lý do model bị ảo giác.
3. Update System Prompt hoặc tinh chỉnh lại *Confidence Threshold* (Ngưỡng tự tin).
4. Review và test lại trên môi trường Staging trước khi bật lại biến môi trường `AI_OCR_MODE = AUTO`.
5. Cập nhật rủi ro mới này vào `risk_register.md`.
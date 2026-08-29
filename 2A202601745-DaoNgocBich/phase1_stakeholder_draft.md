# Phase 1 — Bước 1: Cá nhân liệt kê stakeholder (nháp, chờ Bích duyệt/chỉnh)

> Góc nhìn: Đào Ngọc Bích — AI Engineer / Fullstack & QA.
> Đây là bản nháp AI đề xuất, KHÔNG copy từ Stakeholder Map sẵn có trong
> `PROJECT_OVERVIEW.md` (bản đó nhiều khả năng là góc nhìn của Trang) — mục
> đích Lab là 2 người tự nghĩ độc lập rồi mới gộp ở bước Team. Đọc kỹ, sửa lại
> bất kỳ chỗ nào bạn thấy không đúng với hiểu biết thực tế của bạn về dự án.

## Danh sách 7 stakeholder cụ thể

1. **Ngân hàng Nhà nước Việt Nam (SBV) / cơ quan quản lý fintech** — VPay là
   ví điện tử, mọi cơ chế AI *tự ý* can thiệp/trì hoãn giao dịch tiền đều có
   thể chạm quy định pháp lý về thanh toán. Ảnh hưởng cực cao (quyền phủ
   quyết vận hành thật) nhưng **Interest hiện tại gần bằng 0** vì dự án còn
   ở giai đoạn mô phỏng cho Lab, chưa xin giấy phép trung gian thanh toán →
   xếp **Blocker** (Influence cao / Interest thấp, theo đúng ma trận của
   Lab), chiến lược là chuẩn bị hồ sơ tuân thủ sớm chứ không chỉ theo dõi
   định kỳ như Bystander.
   *(Lưu ý: đây khác với "Ban điều hành VGO/VPay" — người quản lý nội bộ,
   đã có sẵn trong bản của Trang ở nhóm Champion — SBV là bên quản lý pháp
   lý bên ngoài, không trùng vai trò.)*

2. **Trưởng bộ phận An ninh mạng & Compliance nội bộ (VGO)** — người duyệt
   kiến trúc Cổng kép (Blacklist + Risk Engine) có đạt chuẩn bảo mật/độ trễ
   trước khi cho go-live, không phải chỉ xem demo chạy được.

3. **Nhà cung cấp LLM — OpenRouter / Google Gemini (`gemini-2.5-flash`)** —
   external dependency: nếu downtime, đổi giá, hoặc giới hạn rate limit thì
   toàn bộ `fraud_intervention_agent` ngừng hoạt động ngay lập tức. Ảnh hưởng
   cao nhưng team không kiểm soát được.

4. **Đội Vận hành/CSKH (Customer Support)** — người trực tiếp hứng khiếu nại
   khi Risk Engine chấm nhầm (false positive chặn giao dịch hợp lệ của người
   dùng thật), dù họ không tham gia thiết kế model.

5. **SePay (đối tác cổng thanh toán sandbox)** — quyết định khả năng kiểm
   tra STK & nạp tiền thật của toàn bộ luồng demo/pilot; nếu sandbox đổi API
   hoặc giới hạn quota, ảnh hưởng trực tiếp đến khả năng test của team QA.

6. **Người dùng thử thuộc nhóm mục tiêu 32–55 tuổi** — không phải "người
   dùng" chung chung, mà cụ thể là nhóm target chính bị thao túng tâm lý
   nhiều nhất; phản hồi của họ quyết định luồng can thiệp có bị thấy "phiền"
   hay "hữu ích".

7. **Giảng viên/mentor Lab đang chấm Day 27** — có quyền quyết định điểm số
   và mức độ đạt gate của team trong khuôn khổ khóa học này.

## Câu hỏi bạn cần tự trả lời để duyệt bản này — ĐÃ TRẢ LỜI ✅

1. Thiếu ai không? → **Không thiếu**, giữ nguyên 7 stakeholder.
2. Stance thực tế biết chắc? → Chỉ chắc chắn với **Nhà cung cấp LLM
   (OpenRouter/Gemini) = Trung lập** — vendor thương mại, không có thái độ
   ủng hộ/phản đối riêng với VPay. Các stakeholder khác chưa có quan sát
   thực tế đủ tin cậy để gán stance — sẽ để ngỏ, không đoán bừa.
3. Bất đồng nhóm với Trang? → Không, chỉ khác về SBV (đã xử lý ở trên: xếp
   Blocker, không trùng với "Ban điều hành VGO" của Trang).

---

## Trạng thái: Bước 1 (Cá nhân) — HOÀN TẤT

Danh sách 7 stakeholder + 1 điều chỉnh (SBV → Blocker) đã sẵn sàng mang vào
buổi sync Team với Trang để làm Bước 2 (gộp danh sách, đặt lên ma trận
Influence × Interest) và Bước 3 (chọn 4 stakeholder ưu tiên + chiến lược cụ
thể) — 2 bước này là việc của Team, không làm riêng trong thư mục cá nhân.

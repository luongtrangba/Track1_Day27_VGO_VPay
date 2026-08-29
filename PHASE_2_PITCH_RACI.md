# 📑 ARTEFACT 2 — PITCH "KẾT LUẬN TRƯỚC" & RACI MATRIX

> **Dự án:** VPay — Ví điện tử phòng chống lừa đảo chủ động bằng AI (`P-029`)
> **Team:** Lương Thanh Trang (Lead / Product Owner) · Đào Ngọc Bích (AI Engineer / QA)
> **Hình thức:** Team → Cá nhân → Team · 30 phút

---

## 1. 🎯 Chọn stakeholder & Pitch nháp của team (10')

### 1.1. Stakeholder được chọn

**Trưởng BP An ninh Thông tin & Compliance** — lấy từ Phase 1, mục **B1**.

Lý do chọn: đây là stakeholder duy nhất có **stance 🔴 chưa ủng hộ** kèm **Influence cao**. Họ có quyền chặn pilot với dữ liệu thật, tức là chặn luôn con đường lấy bằng chứng thực tế. Ba stakeholder ưu tiên còn lại (Mentor, chuyên gia anti-phishing, nhóm user thử) không có quyền phủ quyết như vậy.

### 1.2. Pitch nháp (bản team, ≤ nửa trang)

> **KẾT LUẬN.** Đề nghị anh/chị duyệt cho VPay chạy pilot giới hạn: **20 tài khoản nội bộ, dữ liệu giả, trong 2 tuần**. Chúng em không xin quyền chạm vào dữ liệu khách hàng thật ở bước này.
>
> **LÝ DO.**
> 1. **Phần lớn giao dịch không có dữ liệu nào rời hệ thống.** Cổng 1 (đối chiếu blacklist) và Cổng 2 (chấm điểm rủi ro bằng Scikit-learn) chạy nội bộ, không gọi LLM. Chỉ khi điểm rủi ro vượt ngưỡng mới mở luồng đối thoại có gọi model bên ngoài.
> 2. **Việc che dữ liệu nhạy cảm nằm trong đường dẫn code, không phải cam kết trên giấy.** Hàm `redact_sensitive_text` / `redact_json_value` / `redact_conversation` (`security.py`) chạy trước khi hội thoại được gửi ra OpenRouter.
> 3. **Rủi ro đã được đo, không phải ước lượng.** Team đã chạy bộ kiểm thử đối kháng và có báo cáo kết quả để anh/chị soi trực tiếp.
>
> **BẰNG CHỨNG.**
> - **Robustness eval — 27/08/2026, 120 lượt hội thoại, 10 nhóm tình huống:** **0 lượt rò rỉ danh tính**, **0 lượt lặp lại giá trị nhạy cảm**, **0 lượt crash**. Trong đó có 18 lượt jailbreak, 11 lượt yêu cầu dữ liệu nhạy cảm và 8 lượt dò danh tính hệ thống — tất cả đều không rò. Điểm liên quan trung bình 0.865.
> - **Chat agent eval — 28/08/2026, 90 ca, 30 kịch bản × 3 lượt:** recall@3 **98.9%**, recall@1 84.4%, MRR 0.916, tỷ lệ đạt ngưỡng 96.7%, độ trễ p95 **2.29 giây**.
> - Hai file báo cáo JSON gốc nằm trong repo, mở ra đọc được từng ca.
>
> **SMALL ASK.** Anh/chị cho em **45 phút ngày 04/09** để trình bày sơ đồ luồng dữ liệu và mở trực tiếp 2 file eval. Cuối buổi em chỉ cần một trong hai: chữ ký duyệt pilot giới hạn, **hoặc** danh sách yêu cầu cụ thể để team đóng trước 11/09.

**Vì sao small ask dừng ở đây:** không xin duyệt toàn hệ thống, không xin dữ liệu thật, không xin ngân sách. Chỉ xin 45 phút và một quyết định nhị phân — đủ nhỏ để họ khó từ chối, đủ lớn để dự án đi tiếp.

---

## 2. 🛡️ Phản biện có khả năng xảy ra nhất & cách xử lý (5')

### Phản biện dự đoán

> **"AI chưa đủ đáng tin. 120 lượt kiểm thử là quá ít để kết luận không rò rỉ dữ liệu. Model bên thứ ba vẫn nằm ngoài tầm kiểm soát của chúng ta — chỉ cần rò một lần là đủ để mất khách hàng."**

Đây là phản biện khả năng cao nhất vì nó tấn công đúng **điểm yếu thật** của bằng chứng hiện có: cỡ mẫu.

### Câu trả lời — dựa trên bằng chứng và hành động giảm rủi ro

**Bước 1 — Thừa nhận đúng phần đúng.** 120 lượt là mẫu nhỏ. Team không nói con số này chứng minh hệ thống an toàn tuyệt đối. Nó chỉ chứng minh: ở 26 lượt tấn công chủ đích (18 jailbreak + 8 dò danh tính), lớp phòng vệ hiện tại **chưa bị phá lần nào**.

**Bước 2 — Đưa cơ chế thay vì lời hứa.** Việc che dữ liệu không dựa vào model tự giác. Nó là bước xử lý bắt buộc chạy **trước** lời gọi API. Model có bị dụ thế nào cũng không thể đọc được thứ chưa từng gửi tới nó.

**Bước 3 — 3 hành động giảm rủi ro, có deadline:**

| # | Hành động giảm rủi ro | Người làm | Hạn |
|:---:|:---|:---|:---|
| 1 | Mở rộng bộ kiểm thử đối kháng từ **120 → 300 lượt**, thêm nhóm tấn công tiêm dữ liệu qua nội dung chuyển khoản | Bích | 25/09/2026 |
| 2 | Thêm **chốt chặn cứng ở tầng code**: nếu bước redact báo lỗi hoặc phát hiện dữ liệu chưa che, hệ thống **không gọi LLM** mà rơi về câu trả lời an toàn | Bích | 18/09/2026 |
| 3 | Ghi log toàn bộ payload thực sự gửi ra ngoài, cấp quyền đọc log cho BP Compliance để tự kiểm bất kỳ lúc nào | Trang | 11/09/2026 |

**Bước 4 — Thu hẹp thiệt hại nếu sai.** Pilot chạy dữ liệu giả trên 20 tài khoản nội bộ. Kịch bản xấu nhất là rò dữ liệu giả của chính team, không phải dữ liệu khách hàng.

---

## 3. ✍️ Bước cá nhân — Mỗi người tự viết lại pitch (5')

Hai thành viên viết riêng, chưa nhìn bản của nhau, để kiểm tra ai thực sự hiểu thông điệp.

### 3.1. Bản của Lương Thanh Trang (góc Product — nói về hậu quả kinh doanh)

> **Kết luận:** Em xin duyệt pilot 20 tài khoản nội bộ, dữ liệu giả, 2 tuần.
> **Lý do:** Cái đắt nhất không phải rủi ro rò dữ liệu giả — mà là mỗi tuần trì hoãn là thêm một tuần người dùng 32–55 tuổi tự tay chuyển tiền cho kẻ lừa đảo mà không có ai hỏi lại họ một câu.
> **Bằng chứng:** 120 lượt kiểm thử đối kháng, 0 rò rỉ. 90 ca kịch bản, agent tìm đúng thủ đoạn trong top 3 ở **98.9%** trường hợp, phản hồi p95 dưới 2.3 giây — đủ nhanh để không ai bỏ ngang giao dịch.
> **Small ask:** 45 phút ngày 04/09, và một quyết định: duyệt, hoặc cho em danh sách điều kiện.

### 3.2. Bản của Đào Ngọc Bích (góc Kỹ thuật — nói về ranh giới dữ liệu)

> **Kết luận:** Đề nghị duyệt pilot giới hạn — dữ liệu giả, 20 tài khoản, 2 tuần.
> **Lý do:** Ranh giới dữ liệu của VPay là ranh giới trong code, không phải trong quy trình. Hai cổng chấm điểm chạy nội bộ; chỉ hội thoại rủi ro cao mới ra ngoài, và ra sau khi đã qua `redact_conversation`.
> **Bằng chứng:** Báo cáo 27/08: 18 lượt jailbreak, 11 lượt đòi dữ liệu nhạy cảm, 8 lượt dò danh tính — **0 rò, 0 crash**. Báo cáo 28/08: 90 ca, tỷ lệ đạt ngưỡng 96.7%.
> **Small ask:** Cho em mở 2 file JSON đó cùng anh/chị trong 45 phút, chỉ vào từng ca. Nếu anh/chị chỉ ra được một ca rò, team dừng và sửa trước khi xin lại.

### 3.3. Câu được team giữ lại cho bản cuối

| Lấy từ | Câu | Vì sao giữ |
|:---|:---|:---|
| Trang | *"Mỗi tuần trì hoãn là thêm một tuần người dùng tự tay chuyển tiền mà không có ai hỏi lại họ một câu."* | Chuyển chi phí của việc **từ chối** sang phía người nghe — trước đó pitch chỉ nói về rủi ro của việc đồng ý |
| Bích | *"Ranh giới dữ liệu nằm trong code, không nằm trong quy trình."* | Một câu chốt được cả lý do 1 và 2, dân kỹ thuật lẫn compliance đều hiểu ngay |
| Bích | *"Nếu anh/chị chỉ ra được một ca rò, team dừng và sửa trước khi xin lại."* | Hạ rủi ro của người duyệt xuống gần 0 — họ không bị khoá vào quyết định |

---

## 4. 📊 RACI Matrix — 6 công việc quan trọng 1–2 tháng tới (10')

**R** — người trực tiếp làm · **A** — người chịu trách nhiệm cuối (mỗi việc đúng 1) · **C** — hỏi ý kiến trước khi quyết · **I** — được thông báo

| # | Công việc (1–2 tháng tới) | Trang<br/>*Lead / PO* | Bích<br/>*AI Eng / QA* | Mentor<br/>*Day 27* | BP An ninh &<br/>Compliance | User thử &<br/>Trusted Contact |
|:---:|:---|:---:|:---:|:---:|:---:|:---:|
| 1 | Whitepaper luồng dữ liệu & giải trình xin duyệt pilot | **A/R** | C | I | **C** | I |
| 2 | Hạ tỷ lệ false-positive: chỉnh ngưỡng Hybrid Risk Engine | **A** | **R** | I | I | **C** |
| 3 | Mở rộng bộ eval đối kháng 120 → 300 lượt | I | **A/R** | **C** | I | — |
| 4 | Bổ sung ≥ 5 kịch bản lừa đảo 2026 vào RAG & đo lại recall | I | **A/R** | C | I | — |
| 5 | Pilot 5 user 32–55 tuổi trong 5 ngày, thu số liệu thực tế | **A/R** | C | I | I | **C** |
| 6 | Quyết định go / no-go: chốt bản demo bảo vệ & release pilot | **A** | **R** | **C** | **C** | I |

### 4.1. Kiểm tra quy tắc

- **Mỗi hàng đúng 1 chữ A** — hàng 1, 2, 5, 6: Trang · hàng 3, 4: Bích. Không hàng nào có 2 A, không hàng nào bỏ trống A.
- **Phân A theo miền chịu hậu quả:** Trang chịu trách nhiệm cuối ở việc đối ngoại và trải nghiệm người dùng; Bích chịu trách nhiệm cuối ở chất lượng model và bộ đo.

### 4.2. Xử lý rủi ro "tự làm — tự duyệt" của team 2 người

Slide khuyến nghị tách R và A. Team chỉ có 2 người nên **2 việc tách được** (hàng 2 và hàng 6: người làm ≠ người chịu trách nhiệm cuối), **4 việc buộc gộp R = A** (hàng 1, 3, 4, 5).

Với 4 việc gộp, team đặt **1 bên ngoài làm C bắt buộc** để không ai vừa làm vừa tự duyệt:

| Việc gộp R = A | Người chặn tự duyệt | Cách chặn cụ thể |
|:---|:---|:---|
| 1 — Whitepaper compliance | BP An ninh & Compliance (C) | Trang không được tự tuyên bố "đã đủ an toàn"; chỉ BP Compliance ký mới tính là đạt |
| 3 — Mở rộng eval | Mentor (C) | Bích gửi bộ ca mới cho mentor duyệt **trước khi** chạy, tránh tự ra đề dễ cho chính mình |
| 4 — Bổ sung kịch bản RAG | Chuyên gia anti-phishing (C) | Kịch bản mới phải do người ngoài team cấp, không do team tự nghĩ |
| 5 — Pilot 5 user | Người dùng thử (C) | Chỉ tính số đo lấy từ thiết bị người dùng thật, không dùng số Trang tự chạy thử |

---

## 🚦 GATE 2 — Pitch rõ, RACI không mơ hồ

- [x] Pitch theo đúng thứ tự **Kết luận → 2–3 lý do → bằng chứng → small ask**, dài dưới nửa trang
- [x] Bằng chứng là **số đo thật** từ 2 báo cáo eval trong repo (27/08 và 28/08/2026), không có con số ước lượng
- [x] Small ask nhỏ và cụ thể: 45 phút ngày 04/09 + một quyết định nhị phân
- [x] Có 1 phản biện khả năng cao nhất, trả lời bằng bằng chứng **và** 3 hành động giảm rủi ro có người làm + hạn
- [x] Có bản pitch cá nhân của cả 2 thành viên, ghi rõ câu nào được giữ lại và vì sao
- [x] RACI có 6 công việc, **mỗi việc đúng 1 Accountable**
- [x] Nêu rõ 2 việc tách được R/A, 4 việc gộp và cách chặn "tự làm tự duyệt" cho từng việc

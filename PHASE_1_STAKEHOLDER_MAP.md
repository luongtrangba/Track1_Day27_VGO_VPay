# 📑 ARTEFACT 1 — STAKEHOLDER MAP & ENGAGEMENT STRATEGY

> **Dự án:** VPay — Ví điện tử phòng chống lừa đảo chủ động bằng AI (`P-029`)
> **Team:** Lương Thanh Trang (Lead / Product Owner) · Đào Ngọc Bích (AI Engineer / QA)
> **Hình thức:** Cá nhân → Team · 20 phút
> **Tuần hành động:** 31/08/2026 → 11/09/2026

---

## 1. 👤 Bước cá nhân — Mỗi thành viên tự liệt kê (5')

Hai thành viên liệt kê riêng, **chưa trao đổi**, để tránh ảnh hưởng lẫn nhau.

### 1.1. Danh sách của Lương Thanh Trang (góc nhìn Product / thị trường)

| # | Stakeholder cụ thể | Vì sao có mặt |
|:---:|:---|:---|
| 1 | Giảng viên / Mentor chấm Lab Day 27 (Track 1) | Người review kiến trúc AI và quyết định điểm bảo vệ |
| 2 | Trưởng bộ phận An ninh Thông tin & Compliance (bên duyệt pilot) | Có quyền phủ quyết việc đưa VPay chạy thử với dữ liệu thật |
| 3 | Nhóm 5 người dùng thử 32–55 tuổi (người thân/bạn của team) | Đối tượng bị lừa đảo nhiều nhất, quyết định app có được dùng thật không |
| 4 | Người thân tin cậy (Trusted Contact) của nhóm user thử | Người nhận cảnh báo chéo — tính năng lõi phụ thuộc họ |
| 5 | Đối tác cổng thanh toán SePay (sandbox) | Cấp webhook đối soát & tra cứu STK cho luồng nạp/chuyển tiền |
| 6 | Nhà đầu tư / quỹ seed fintech tiềm năng | Nguồn vốn giai đoạn sau khi có số liệu pilot |
| 7 | Các team cùng lớp Track 1 | Nguồn phản biện chéo trước buổi bảo vệ |

### 1.2. Danh sách của Đào Ngọc Bích (góc nhìn Kỹ thuật / vận hành AI)

| # | Stakeholder cụ thể | Vì sao có mặt |
|:---:|:---|:---|
| 1 | Core Team — Trang (Lead/PO) & Bích (AI Eng/QA) | Người trực tiếp build, chịu mọi rủi ro kỹ thuật |
| 2 | Nhà cung cấp LLM & hạ tầng: OpenRouter (`gemini-2.5-flash`) + Neon Postgres/pgvector | Toàn bộ `fraud_intervention_agent` và RAG dừng nếu hai dịch vụ này gián đoạn |
| 3 | Chuyên gia / cộng đồng anti-phishing (nguồn 30 kịch bản lừa đảo + blacklist) | Cung cấp dữ liệu và làm giàu knowledge base RAG |
| 4 | Trưởng BP An ninh Thông tin & Compliance | Yêu cầu redact PII trước khi dữ liệu rời hệ thống |
| 5 | Nhóm user thử 32–55 tuổi | Nguồn dữ liệu false-positive thực tế để tinh chỉnh Risk Engine |
| 6 | Giảng viên / Mentor Day 27 | Đặt chuẩn evals & benchmark team phải đạt |
| 7 | Cơ quan quản lý (NHNN, Cục An toàn thông tin) | Khung pháp lý eKYC / dữ liệu cá nhân khi sản phẩm rời giai đoạn mô phỏng |

**Kết quả gộp:** 14 mục cá nhân → loại 4 mục trùng (Mentor, Compliance, User 32–55, Core Team) → **11 stakeholder cụ thể** đưa vào map.

---

## 2. 🗂️ Bước team — Bảng stakeholder hợp nhất (7')

Hai trục chấm nhị phân **Cao / Thấp** để đặt dứt khoát vào 1 ô. Cột *Stance* ghi thái độ **thực tế đang quan sát được**, không suy ra từ nhãn quadrant.

| # | Stakeholder cụ thể | Influence | Interest | Quadrant (nhãn slide) | Stance thực tế |
|:---:|:---|:---:|:---:|:---:|:---|
| 1 | Giảng viên / Mentor chấm Lab Day 27 | Cao | Cao | **Champion** | 🟢 Ủng hộ |
| 2 | Core Team — Trang (Lead/PO) & Bích (AI Eng/QA) | Cao | Cao | **Champion** | 🟢 Ủng hộ |
| 3 | Trưởng BP An ninh Thông tin & Compliance | Cao | Cao | **Champion** *(nhãn)* | 🔴 **Chưa ủng hộ** — xem §2.2 |
| 4 | Nhóm 5 user thử 32–55 tuổi | Cao | Thấp | **Blocker** | 🟡 Trung lập, ngại bị làm phiền |
| 5 | Đối tác SePay (sandbox webhook) | Cao | Thấp | **Blocker** | 🟡 Trung lập |
| 6 | OpenRouter + Neon (LLM & vector DB) | Cao | Thấp | **Blocker** | 🟡 Trung lập — xem §2.2 |
| 7 | Người thân tin cậy (Trusted Contact) | Thấp | Cao | **Supporter** | 🟢 Ủng hộ mạnh |
| 8 | Chuyên gia / cộng đồng anti-phishing | Thấp | Cao | **Supporter** | 🟢 Ủng hộ |
| 9 | Các team cùng lớp Track 1 (peer review) | Thấp | Cao | **Supporter** | 🟢 Ủng hộ |
| 10 | Cơ quan quản lý (NHNN / Cục ATTT) | Thấp | Thấp | **Bystander** | 🟡 Trung lập |
| 11 | Nhà đầu tư / quỹ seed fintech | Thấp | Thấp | **Bystander** | 🟡 Trung lập |

### 2.1. Ma trận Influence × Interest

```
             ▲ INFLUENCE (mức độ ảnh hưởng)
             │
             │  BLOCKER — ưu tiên thuyết phục      │  CHAMPION — ủng hộ chủ chốt
             │  (giữ hài lòng, xử lý mối lo)       │  (làm việc chặt, tận dụng ủng hộ)
        CAO  │  • User thử 32–55 tuổi        🟡    │  • Mentor Day 27               🟢
             │  • Đối tác SePay             🟡    │  • Core Team (Trang & Bích)    🟢
             │  • OpenRouter + Neon         🟡    │  • BP An ninh & Compliance     🔴 ⚠
             ├─────────────────────────────────────┼──────────────────────────────────────
             │  BYSTANDER — theo dõi định kỳ       │  SUPPORTER — giữ thông tin,
             │                                     │  khai thác feedback
       THẤP  │  • NHNN / Cục ATTT           🟡    │  • Người tin cậy (Trusted)     🟢
             │  • Nhà đầu tư seed           🟡    │  • Chuyên gia anti-phishing    🟢
             │                                     │  • Team cùng lớp Track 1       🟢
             └─────────────────────────────────────┴──────────────────────────────────────►
                          THẤP                                    CAO
                                INTEREST (mức độ quan tâm)

   Stance:  🟢 Ủng hộ   🟡 Trung lập   🔴 Chưa ủng hộ / phản đối
   ⚠ = stance thực tế lệch khỏi nhãn quadrant
```

### 2.2. Hai trường hợp stance lệch nhãn quadrant — ghi nhận thực tế

| Stakeholder | Nhãn quadrant gợi ý | Thực tế | Lý do lệch |
|:---|:---|:---|:---|
| **BP An ninh & Compliance** (#3) | Champion — vì Influence cao, Interest cao | 🔴 **Chưa ủng hộ** | Họ quan tâm cao **theo hướng ngược**: quan tâm vì lo rủi ro, không phải vì muốn dự án thành công. Mối lo chính là PII giao dịch bị đẩy ra LLM bên thứ ba (OpenRouter). Interest cao ≠ ủng hộ, nên vẫn phải xử lý như *người cần ưu tiên thuyết phục* dù ngồi ở ô Champion. |
| **OpenRouter + Neon** (#6) | Blocker — vì Influence cao, Interest thấp | 🟡 Trung lập | Họ không chủ động cản, nhưng là **single point of failure**: rate-limit hoặc đổi giá model là chặn được cả `fraud_intervention_agent`. Ảnh hưởng đến từ phụ thuộc kỹ thuật, không đến từ thái độ — nên cách xử lý là giảm phụ thuộc, không phải thuyết phục. |

---

## 3. 🎯 Bước team — 4 stakeholder ưu tiên & chiến lược (8')

### 🌟 Nhóm A — 2 stakeholder đang ủng hộ mạnh (tận dụng sức ảnh hưởng)

**A1. Giảng viên / Mentor chấm Lab Day 27** — Champion · 🟢 Ủng hộ

| | |
|:---|:---|
| **Quan tâm điều gì** | Kiến trúc agent có kiểm chứng được không: bộ eval, độ trễ chat, cách team tách R/A khi chỉ có 2 người |
| **Giúp / cản thế nào** | *Giúp:* chốt hướng bảo vệ, giới thiệu mentor mảng bảo mật để phản biện. *Cản:* nếu thấy số liệu không có bằng chứng, điểm kiến trúc bị trừ và team mất buổi review |
| **Hành động 1–2 tuần** | **Trước 17h Thứ Sáu 04/09:** Bích chạy `pytest --collect-only -q` và bộ eval trong `evals/agents/`, xuất **file kết quả eval thật** (số ca pass/fail, độ trễ p95 luồng chat) — không dùng số ước lượng. Trang gửi kèm video demo 90 giây luồng can thiệp và đặt lịch 1-1 30 phút **Thứ Ba 08/09** để mentor chốt phương án bảo vệ, đồng thời xin giới thiệu 1 mentor mảng bảo mật |

**A2. Chuyên gia / cộng đồng anti-phishing** — Supporter · 🟢 Ủng hộ

| | |
|:---|:---|
| **Quan tâm điều gì** | Kịch bản lừa đảo trong knowledge base có đúng thủ đoạn đang chạy ngoài thực tế không; muốn dữ liệu họ đóng góp được dùng đúng mục đích |
| **Giúp / cản thế nào** | *Giúp:* bổ sung kịch bản mới và blacklist STK/đầu số, tăng độ phủ RAG. *Cản:* nếu bỏ mặc, kho 30 kịch bản cũ dần, agent trả lời lệch thủ đoạn hiện hành |
| **Hành động 1–2 tuần** | **Trước Thứ Bảy 05/09:** Bích đóng gói 30 kịch bản hiện có thành bản tóm tắt 1 trang, gửi 3 chuyên gia/admin group anti-phishing xin bổ sung **tối thiểu 5 kịch bản mới trong năm 2026**; nạp vào pgvector và đo lại recall RAG **trước Thứ Sáu 11/09** |

### ⚠️ Nhóm B — 2 stakeholder chưa ủng hộ / có rủi ro cản trở (ưu tiên thuyết phục)

**B1. Trưởng BP An ninh Thông tin & Compliance** — ô Champion nhưng · 🔴 Chưa ủng hộ

| | |
|:---|:---|
| **Quan tâm điều gì** | PII (số tài khoản, số tiền, nội dung chuyển khoản) bị gửi ra LLM bên thứ ba; chưa có bằng chứng dữ liệu được che trước khi rời hệ thống |
| **Giúp / cản thế nào** | *Cản:* có quyền chặn pilot với dữ liệu thật → dự án kẹt ở mức mô phỏng. *Giúp:* nếu duyệt, mở đường chạy thử nội bộ và cho phép dùng chuẩn bảo mật của họ làm điểm mạnh khi pitch |
| **Hành động 1–2 tuần** | **Trước Thứ Tư 02/09:** Trang soạn whitepaper 2 trang gồm (a) sơ đồ luồng dữ liệu chỉ rõ điểm redact PII trước khi gọi OpenRouter, (b) chứng minh Cổng 1 blacklist và Cổng 2 Scikit-learn chạy **nội bộ, không gọi LLM**, (c) danh sách trường dữ liệu không bao giờ rời hệ thống. **Thứ Sáu 04/09** họp 45 phút giải trình. Kết quả cần đạt: văn bản đồng ý pilot có điều kiện, hoặc danh sách yêu cầu cụ thể để team đóng trước 11/09 |

**B2. Nhóm 5 user thử 32–55 tuổi** — Blocker · 🟡 Trung lập, ngại bị làm phiền

| | |
|:---|:---|
| **Quan tâm điều gì** | Chuyển tiền phải nhanh và không bị hỏi vặn; sợ app bắt trả lời câu hỏi ở mỗi lần giao dịch |
| **Giúp / cản thế nào** | *Cản:* nếu can thiệp sai (false-positive) vài lần, họ bỏ app — mất luôn nguồn dữ liệu hành vi. *Giúp:* nếu giữ được, họ là bằng chứng thực tế mạnh nhất khi trình bày với mentor và nhà đầu tư |
| **Hành động 1–2 tuần** | **Trước Chủ Nhật 06/09:** Bích đặt ngưỡng Hybrid Risk Engine — giao dịch quen thuộc dưới 5 triệu đi thẳng, chỉ mở đối thoại can thiệp khi điểm rủi ro > 75/100, luôn có nút "Tôi hiểu rủi ro, tiếp tục". **Từ 07/09 đến 11/09:** Trang cho 5 người dùng thật trong 5 ngày, ghi nhận **số lần bị hỏi / tổng số giao dịch** và thu 5 phản hồi ngắn; nếu tỷ lệ bị hỏi vượt 20% thì nâng ngưỡng trước khi demo |

---

## 4. 📌 Ghi chú trung thực về số liệu

Team **chưa** có benchmark công bố được cho tỷ lệ phát hiện gian lận và tỷ lệ false-positive. Mọi con số đưa vào Artefact 2 (Pitch) chỉ dùng kết quả đo được từ `evals/` và 5 ngày dùng thật ở hành động B2. Trước khi có số, pitch mô tả **cơ chế**, không hứa **tỷ lệ**.

---

## 🚦 GATE 1 — Stakeholder Map có thể hành động

- [x] Mỗi thành viên tự liệt kê ≥ 6 stakeholder cụ thể trước khi thảo luận (Trang 7, Bích 7)
- [x] Đã gộp và loại trùng → 11 stakeholder cụ thể, không có mục chung chung
- [x] Map theo Influence × Interest, **cả 4 góc phần tư đều có người**
- [x] Có stance thực tế 🟢/🟡/🔴 cho từng stakeholder
- [x] 2 trường hợp stance lệch nhãn quadrant được ghi nhận kèm lý do (§2.2)
- [x] 4 hành động cụ thể — có người làm, việc làm, con số cần đạt và deadline

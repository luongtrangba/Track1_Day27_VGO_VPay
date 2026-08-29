# 📑 ARTEFACT 1 — STAKEHOLDER MAP & ENGAGEMENT STRATEGY

> **Dự án:** VPay — Ví điện tử phòng chống lừa đảo chủ động bằng AI (`P-029`)
> **Team:** Lương Thanh Trang (Lead / Product Owner) · Đào Ngọc Bích (AI Engineer / QA)
> **Hình thức:** Cá nhân → Team · 20 phút
> **Tuần hành động:** 31/08/2026 → 11/09/2026

---

## 1. 👤 Bước cá nhân — Mỗi thành viên tự liệt kê (5')

Hai thành viên liệt kê riêng, **chưa trao đổi**. Bản gốc của Bích được giữ nguyên tại [`2A202601745-DaoNgocBich/phase1_stakeholder_draft.md`](./2A202601745-DaoNgocBich/phase1_stakeholder_draft.md) để đối chiếu.

### 1.1. Danh sách của Lương Thanh Trang — 8 mục (góc Product / thị trường)

| # | Stakeholder cụ thể | Vì sao có mặt |
|:---:|:---|:---|
| T1 | Giảng viên / Mentor chấm Lab Day 27 (Track 1) | Người review kiến trúc AI và quyết định mức đạt gate |
| T2 | Trưởng BP An ninh Thông tin & Compliance nội bộ (VGO) | Có quyền phủ quyết việc đưa VPay chạy thử với dữ liệu thật |
| T3 | Nhóm 5 người dùng thử 32–55 tuổi | Đối tượng bị lừa đảo nhiều nhất, quyết định app có được dùng thật không |
| T4 | Người thân tin cậy (Trusted Contact) của nhóm user thử | Người nhận cảnh báo chéo — tính năng lõi phụ thuộc họ |
| T5 | Đối tác cổng thanh toán SePay (sandbox) | Cấp webhook đối soát và tra cứu STK cho luồng nạp/chuyển tiền |
| T6 | Chuyên gia / cộng đồng anti-phishing | Nguồn 30 kịch bản lừa đảo và blacklist STK / đầu số |
| T7 | Nhà đầu tư / quỹ seed fintech tiềm năng | Nguồn vốn giai đoạn sau khi có số liệu pilot |
| T8 | Các team cùng lớp Track 1 | Nguồn phản biện chéo trước buổi bảo vệ |

### 1.2. Danh sách của Đào Ngọc Bích — 7 mục (góc Kỹ thuật / vận hành AI)

*Nguyên văn từ file cá nhân của Bích, không sửa nội dung.*

| # | Stakeholder cụ thể | Vì sao có mặt (lập luận của Bích) |
|:---:|:---|:---|
| B1 | **Ngân hàng Nhà nước Việt Nam (SBV) / cơ quan quản lý fintech** | VPay là ví điện tử; mọi cơ chế AI *tự ý* can thiệp hoặc trì hoãn giao dịch tiền đều có thể chạm quy định pháp lý về thanh toán. **Khác với Ban điều hành VGO nội bộ** — đây là bên quản lý pháp lý bên ngoài |
| B2 | Trưởng BP An ninh mạng & Compliance nội bộ (VGO) | Người duyệt kiến trúc Cổng kép có đạt chuẩn bảo mật và độ trễ trước khi go-live, không phải chỉ xem demo chạy được |
| B3 | Nhà cung cấp LLM — OpenRouter / Google Gemini (`gemini-2.5-flash`) | Phụ thuộc bên ngoài: downtime, đổi giá hoặc rate limit là `fraud_intervention_agent` ngừng ngay. Ảnh hưởng cao, team không kiểm soát được |
| B4 | **Đội Vận hành / CSKH (Customer Support)** | Người trực tiếp hứng khiếu nại khi Risk Engine chấm nhầm giao dịch hợp lệ, dù họ không tham gia thiết kế model |
| B5 | SePay (đối tác cổng thanh toán sandbox) | Nếu sandbox đổi API hoặc siết quota, ảnh hưởng thẳng đến khả năng test của QA |
| B6 | Người dùng thử nhóm mục tiêu 32–55 tuổi | Không phải "người dùng" chung chung — nhóm bị thao túng tâm lý nhiều nhất; phản hồi của họ quyết định luồng can thiệp là "phiền" hay "hữu ích" |
| B7 | Giảng viên / mentor Lab đang chấm Day 27 | Quyết định điểm số và mức đạt gate của team |

### 1.3. Kết quả gộp

15 mục cá nhân → **4 mục trùng** (Mentor: T1≡B7 · Compliance nội bộ: T2≡B2 · User 32–55: T3≡B6 · SePay: T5≡B5) → **11 stakeholder** đưa vào map.

**Hai mục chỉ Bích nhìn ra, team giữ nguyên cả hai:**

| Mục riêng của Bích | Vì sao team chấp nhận đưa vào |
|:---|:---|
| **SBV / cơ quan quản lý fintech** (B1) | Bản của Trang chỉ có Compliance *nội bộ*. Bích tách đúng: nội bộ duyệt kiến trúc, còn cơ quan quản lý cấp phép trung gian thanh toán — hai người khác nhau, quyền khác nhau |
| **Đội Vận hành / CSKH** (B4) | Không ai trong bản của Trang nghĩ tới người **hứng hậu quả** của false-positive. Đây là stakeholder duy nhất chịu thiệt trực tiếp mỗi lần model chấm sai |

---

## 2. 🗂️ Bước team — Bảng stakeholder hợp nhất (7')

Hai trục chấm nhị phân **Cao / Thấp** để đặt dứt khoát vào 1 ô. Cột **Nguồn** ghi ai đề xuất. Cột **Cơ sở stance** áp dụng nguyên tắc Bích đặt ra: *"chưa có quan sát thực tế đủ tin cậy thì để ngỏ, không đoán bừa"*.

| # | Stakeholder cụ thể | Nguồn | Influence | Interest | Quadrant | Stance | Cơ sở stance |
|:---:|:---|:---:|:---:|:---:|:---:|:---|:---|
| 1 | Giảng viên / Mentor chấm Lab Day 27 | T+B | Cao | Cao | **Champion** | 🟢 Ủng hộ | ✅ Đã quan sát |
| 2 | Trưởng BP An ninh & Compliance nội bộ (VGO) | T+B | Cao | Cao | **Champion** *(nhãn)* | 🔴 Chưa ủng hộ | ⚠️ Giả định |
| 3 | **SBV / cơ quan quản lý fintech** | **B** | Cao | Thấp | **Blocker** | 🟡 Trung lập | ⚠️ Giả định |
| 4 | Nhóm 5 user thử 32–55 tuổi | T+B | Cao | Thấp | **Blocker** | 🟡 Ngại bị làm phiền | ⚠️ Giả định |
| 5 | OpenRouter / Gemini (+ Neon pgvector) | **B** | Cao | Thấp | **Blocker** | 🟡 Trung lập | ✅ **Chắc chắn** — vendor thương mại, không có thái độ riêng với VPay |
| 6 | SePay (sandbox webhook) | T+B | Cao | Thấp | **Blocker** | 🟡 Trung lập | ⚠️ Giả định |
| 7 | **Đội Vận hành / CSKH** | **B** | Thấp | Cao | **Supporter** | 🟡 Lo tăng khiếu nại | ⚠️ Giả định |
| 8 | Người thân tin cậy (Trusted Contact) | T | Thấp | Cao | **Supporter** | 🟢 Ủng hộ | ⚠️ Giả định |
| 9 | Chuyên gia / cộng đồng anti-phishing | T | Thấp | Cao | **Supporter** | 🟢 Ủng hộ | ⚠️ Giả định |
| 10 | Các team cùng lớp Track 1 | T | Thấp | Cao | **Supporter** | 🟢 Ủng hộ | ✅ Đã quan sát |
| 11 | Nhà đầu tư / quỹ seed fintech | T | Thấp | Thấp | **Bystander** | 🟡 Trung lập | ✅ Chắc chắn — chưa từng tiếp xúc |

### 2.1. Ma trận Influence × Interest

```
             ▲ INFLUENCE (mức độ ảnh hưởng)
             │
             │  BLOCKER — ưu tiên thuyết phục      │  CHAMPION — ủng hộ chủ chốt
             │  (giữ hài lòng, xử lý mối lo)       │  (làm việc chặt, tận dụng ủng hộ)
        CAO  │  • SBV / quản lý fintech      🟡    │  • Mentor Day 27              🟢
             │  • User thử 32–55 tuổi        🟡    │  • BP An ninh & Compliance    🔴 ⚠
             │  • OpenRouter / Gemini        🟡    │
             │  • SePay sandbox              🟡    │
             ├─────────────────────────────────────┼──────────────────────────────────────
             │  BYSTANDER — theo dõi định kỳ       │  SUPPORTER — giữ thông tin,
             │                                     │  khai thác feedback
       THẤP  │  • Nhà đầu tư seed            🟡    │  • Đội Vận hành / CSKH        🟡
             │                                     │  • Người tin cậy (Trusted)    🟢
             │                                     │  • Chuyên gia anti-phishing   🟢
             │                                     │  • Team cùng lớp Track 1      🟢
             └─────────────────────────────────────┴──────────────────────────────────────►
                          THẤP                                    CAO
                                INTEREST (mức độ quan tâm)

   Stance:  🟢 Ủng hộ   🟡 Trung lập   🔴 Chưa ủng hộ / phản đối
   ⚠ = stance thực tế lệch khỏi nhãn quadrant
```

### 2.2. Ba trường hợp nhãn quadrant dễ gây hiểu sai

| Stakeholder | Nhãn quadrant | Thực tế | Xử lý |
|:---|:---|:---|:---|
| **BP An ninh & Compliance** (#2) | Champion — Influence cao × Interest cao | 🔴 **Chưa ủng hộ** | Họ quan tâm cao **theo hướng ngược**: quan tâm vì lo rủi ro PII, không phải vì muốn dự án thành công. *Interest cao ≠ ủng hộ.* Vẫn phải xử lý như người cần ưu tiên thuyết phục dù ngồi ở ô Champion |
| **SBV / cơ quan quản lý** (#3) | Blocker — Influence cao × Interest thấp | 🟡 Trung lập | **Lập luận của Bích, team giữ nguyên:** Interest gần bằng 0 vì dự án còn ở giai đoạn mô phỏng, chưa xin giấy phép trung gian thanh toán. Nhưng chiến lược **không phải "theo dõi định kỳ" kiểu Bystander** — họ có quyền phủ quyết vận hành thật, nên phải chuẩn bị hồ sơ tuân thủ sớm |
| **OpenRouter / Gemini** (#5) | Blocker — Influence cao × Interest thấp | 🟡 Trung lập | Không chủ động cản, nhưng là **single point of failure**: rate-limit hoặc đổi giá là chặn được cả agent. Ảnh hưởng đến từ phụ thuộc kỹ thuật, không từ thái độ → xử lý bằng **giảm phụ thuộc** (dự phòng model thứ hai), không phải thuyết phục |

### 2.3. Độ tin cậy của stance — 8/11 mục vẫn là giả định

Nguyên tắc Bích đặt: chỉ 3 stance dựa trên tiếp xúc thật (Mentor, OpenRouter, Nhà đầu tư). **8 mục còn lại là giả định làm việc**, phải kiểm chứng trước khi dùng làm căn cứ ra quyết định:

| Cần kiểm chứng | Cách kiểm | Hạn |
|:---|:---|:---|
| Compliance có thực sự phản đối, hay chỉ chưa được trình bày? | Buổi giải trình 45 phút | 04/09/2026 |
| User 32–55 thấy can thiệp là "phiền" hay "hữu ích"? | 5 ngày pilot, đo số lần bị hỏi / tổng giao dịch | 11/09/2026 |
| Trusted Contact có thật sự muốn nhận cảnh báo? | Gửi bản thử cho 5 người, thu phản hồi | 06/09/2026 |
| Đội CSKH lo ngại tới mức nào? | Hỏi 1 buổi 20 phút về khối lượng khiếu nại hiện tại | 09/09/2026 |
| SBV nhìn cơ chế can thiệp thế nào? | Rà quy định trung gian thanh toán, chưa tiếp xúc trực tiếp | 30/09/2026 |

Trước các mốc trên, mọi ô 🟡/🔴 giả định được ghi là *giả định*, không được trình bày với Mentor như sự thật đã xác nhận.

---

## 3. 🎯 Bước team — 4 stakeholder ưu tiên & chiến lược (8')

### 🌟 Nhóm A — 2 stakeholder đang ủng hộ mạnh (tận dụng sức ảnh hưởng)

**A1. Giảng viên / Mentor chấm Lab Day 27** — Champion · 🟢 Ủng hộ ✅ *(stance đã quan sát)*

| | |
|:---|:---|
| **Quan tâm điều gì** | Kiến trúc agent có kiểm chứng được không: bộ eval, độ trễ chat, cách team tách R/A khi chỉ có 2 người |
| **Giúp / cản thế nào** | *Giúp:* chốt hướng bảo vệ, giới thiệu mentor mảng bảo mật để phản biện. *Cản:* nếu thấy số liệu không có bằng chứng, điểm kiến trúc bị trừ và team mất buổi review |
| **Hành động 1–2 tuần** | **Trước 17h Thứ Sáu 04/09:** Bích gửi 2 báo cáo eval thật đã có trong repo (90 ca chat agent 28/08 · 120 lượt đối kháng 27/08) kèm số `pytest --collect-only` = 1560 test. Trang gửi video demo 90 giây luồng can thiệp, đặt lịch 1-1 30 phút **Thứ Ba 08/09** để mentor chốt phương án bảo vệ và xin giới thiệu 1 mentor mảng bảo mật |

**A2. Chuyên gia / cộng đồng anti-phishing** — Supporter · 🟢 Ủng hộ ⚠️ *(stance là giả định — buổi tiếp xúc đầu tiên cũng chính là bước kiểm chứng)*

| | |
|:---|:---|
| **Quan tâm điều gì** | Kịch bản trong knowledge base có đúng thủ đoạn đang chạy ngoài thực tế không; muốn dữ liệu họ đóng góp được dùng đúng mục đích |
| **Giúp / cản thế nào** | *Giúp:* bổ sung kịch bản mới và blacklist STK/đầu số, tăng độ phủ RAG. *Cản:* nếu bỏ mặc, kho 30 kịch bản cũ dần, agent trả lời lệch thủ đoạn hiện hành |
| **Hành động 1–2 tuần** | **Trước Thứ Bảy 05/09:** Bích đóng gói 30 kịch bản hiện có thành bản tóm tắt 1 trang, gửi 3 chuyên gia / admin group anti-phishing xin bổ sung **tối thiểu 5 kịch bản mới năm 2026**; nạp vào pgvector và đo lại recall RAG **trước Thứ Sáu 11/09**. Ghi nhận luôn stance thật của họ sau lần liên hệ đầu |

### ⚠️ Nhóm B — 2 stakeholder chưa ủng hộ / có rủi ro cản trở (ưu tiên thuyết phục)

**B1. Trưởng BP An ninh Thông tin & Compliance nội bộ** — ô Champion nhưng · 🔴 Chưa ủng hộ

| | |
|:---|:---|
| **Quan tâm điều gì** | PII (số tài khoản, số tiền, nội dung chuyển khoản) bị gửi ra LLM bên thứ ba; chưa có bằng chứng dữ liệu được che trước khi rời hệ thống. Theo Bích: họ duyệt **kiến trúc Cổng kép đạt chuẩn bảo mật và độ trễ**, không phải duyệt một bản demo chạy được |
| **Giúp / cản thế nào** | *Cản:* có quyền chặn pilot với dữ liệu thật → dự án kẹt ở mức mô phỏng. *Giúp:* nếu duyệt, mở đường chạy thử nội bộ và cho phép dùng chuẩn bảo mật của họ làm điểm mạnh khi pitch |
| **Hành động 1–2 tuần** | **Trước Thứ Tư 02/09:** Trang soạn whitepaper 2 trang gồm (a) sơ đồ luồng dữ liệu chỉ rõ điểm redact PII trước khi gọi OpenRouter, (b) chứng minh Cổng 1 blacklist và Cổng 2 Scikit-learn chạy **nội bộ, không gọi LLM**, (c) danh sách trường dữ liệu không bao giờ rời hệ thống, (d) số độ trễ p95 đo được. **Thứ Sáu 04/09** họp 45 phút giải trình. Kết quả cần đạt: văn bản đồng ý pilot có điều kiện, **hoặc** danh sách yêu cầu cụ thể để team đóng trước 11/09 |

**B2. Nhóm 5 user thử 32–55 tuổi** — Blocker · 🟡 Ngại bị làm phiền

| | |
|:---|:---|
| **Quan tâm điều gì** | Chuyển tiền phải nhanh và không bị hỏi vặn; sợ app bắt trả lời câu hỏi ở mỗi lần giao dịch |
| **Giúp / cản thế nào** | *Cản:* nếu can thiệp sai vài lần, họ bỏ app — mất luôn nguồn dữ liệu hành vi, và **đội CSKH (#7) là bên hứng khiếu nại**. *Giúp:* nếu giữ được, họ là bằng chứng thực tế mạnh nhất khi trình bày với Mentor và nhà đầu tư |
| **Hành động 1–2 tuần** | **Trước Chủ Nhật 06/09:** Bích đặt ngưỡng Hybrid Risk Engine — giao dịch quen thuộc dưới 5 triệu đi thẳng, chỉ mở đối thoại can thiệp khi điểm rủi ro > 75/100, luôn có nút "Tôi hiểu rủi ro, tiếp tục". **Từ 07/09 đến 11/09:** Trang cho 5 người dùng thật trong 5 ngày, ghi nhận **số lần bị hỏi / tổng số giao dịch**, thu 5 phản hồi ngắn; nếu tỷ lệ bị hỏi vượt 20% thì nâng ngưỡng trước khi demo |

### Vì sao 2 stakeholder mới của Bích chưa vào top 4

| Stakeholder | Lý do chưa ưu tiên trong 2 tuần này | Việc phải làm sau |
|:---|:---|:---|
| **SBV / cơ quan quản lý** | Cần trước khi vận hành thật với tiền thật; giai đoạn hiện tại còn là dữ liệu giả nên chưa phải nút thắt của 2 tuần tới | Rà quy định trung gian thanh toán, dựng khung hồ sơ tuân thủ — hạn 30/09/2026, Trang phụ trách |
| **Đội Vận hành / CSKH** | Chưa có người dùng thật nên chưa có khiếu nại để họ hứng | Sau pilot 11/09, đưa số "số lần bị hỏi / tổng giao dịch" cho họ ước lượng tải khiếu nại — hạn 18/09/2026, Trang phụ trách |

---

## 4. 📌 Ràng buộc trung thực về số liệu

Theo chốt ở Phase 0: hai con số **>95% detection** và **<3% false-positive** là *target chưa đo*, **không được dùng làm bằng chứng** trong Artefact 2. Bằng chứng hợp lệ duy nhất là kết quả đo thật trong `evals/` (90 ca chat agent, 120 lượt đối kháng, 1560 test) và số liệu 5 ngày pilot ở hành động B2.

---

## 🚦 GATE 1 — Stakeholder Map có thể hành động

- [x] Mỗi thành viên tự liệt kê ≥ 6 stakeholder cụ thể trước khi thảo luận (Trang 8 · Bích 7, file gốc lưu trong repo)
- [x] Đã gộp và loại 4 mục trùng → **11 stakeholder cụ thể**, không có mục chung chung
- [x] Ghi rõ 2 stakeholder chỉ 1 người nhìn ra (SBV, Đội CSKH) và lý do team giữ lại
- [x] Map theo Influence × Interest, **cả 4 góc phần tư đều có người**
- [x] Có stance 🟢/🟡/🔴 cho từng stakeholder, **kèm cơ sở stance** — phân biệt rõ đã quan sát vs. còn là giả định
- [x] 3 trường hợp nhãn quadrant dễ hiểu sai được giải thích và ghi cách xử lý khác nhau (§2.2)
- [x] 8 stance giả định có kế hoạch kiểm chứng kèm hạn (§2.3)
- [x] 4 hành động cụ thể — có người làm, việc làm, con số cần đạt và deadline

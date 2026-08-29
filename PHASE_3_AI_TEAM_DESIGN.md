# 📑 ARTEFACT 3 — AI TEAM ARCHITECTURE & PRIORITY RESOURCING

> **Dự án:** VPay — Ví điện tử phòng chống lừa đảo chủ động bằng AI (`P-029`)
> **Team:** Lương Thanh Trang (Lead / Product Owner) · Đào Ngọc Bích (AI Engineer / QA)
> **Hình thức:** Team · 25 phút

---

## 1. 🏗️ Chọn AI Team Architecture (5')

### Quyết định: **EMBEDDED**

> Năng lực AI **nằm trực tiếp trong team sản phẩm** — người viết `fraud_intervention_agent` cũng là người viết API ví và chạy eval, không có tầng trung gian nào ở giữa.

**Vì sao Embedded, không phải Hybrid hay Centralized:**

1. **Không có gì để tập trung hoá.** Centralized và Hybrid chỉ có nghĩa khi có **nhiều sản phẩm** cùng dùng chung năng lực AI. VPay là sản phẩm duy nhất, team 2 người — dựng "hub AI" chung là dựng một tầng phục vụ chính mình.
2. **Vòng lặp sửa lỗi phải ngắn.** Điểm rủi ro lớn nhất hiện tại là false-positive làm phiền người dùng. Người phát hiện, người sửa ngưỡng và người chạy lại eval phải là **cùng một người trong cùng một ngày**. Bất kỳ tầng bàn giao nào cũng kéo dài vòng này.

> ⚠️ **Chỉnh lại tài liệu cũ:** `PROJECT_OVERVIEW.md` mục 4 và `README.md` từng ghi mô hình là *Hybrid*. Sau khi rà quy mô thật (2 người, 1 sản phẩm), team chốt lại là **Embedded**. Hybrid chỉ đúng khi VPay tách thành nhiều sản phẩm hoặc có team thứ hai dùng lại risk engine.

**Điều kiện để đổi sang Hybrid:** khi Hybrid Risk Engine được team/sản phẩm thứ hai gọi lại, hoặc khi team vượt 6 người. Cả hai đều chưa xảy ra.

```
        ┌─────────────────── SQUAD VPay (Embedded) ───────────────────┐
        │                                                             │
        │   Trang — Lead / Product Owner       Bích — AI Eng / QA      │
        │   • Sở hữu bài toán chống lừa đảo    • Agent LangGraph       │
        │   • Stakeholder & Compliance         • RAG pgvector          │
        │   • Trải nghiệm can thiệp (UX)       • Risk Engine + Evals   │
        │   • Pilot & số liệu người dùng       • Backend / DB          │
        │                                                             │
        │        Không có tầng AI hub trung gian — 0 bước bàn giao     │
        └──────────────┬──────────────────────────┬───────────────────┘
                       │                          │
              ┌────────▼────────┐        ┌────────▼────────┐
              │ Năng lực MƯỢN    │        │ Năng lực THUÊ   │
              │ ngoài (Partner)  │        │ ngoài (Outsource)│
              │ • Compliance     │        │ • Sản xuất FMV  │
              │ • Chuyên gia     │        │                 │
              │   anti-phishing  │        │                 │
              └─────────────────┘        └─────────────────┘
```

---

## 2. 👥 Core Roles & Extended Roles (8')

### 2.1. CORE — vai trò cần **ngay** ở giai đoạn hiện tại

| Vai trò cốt lõi | Vì sao cần ngay | Ai đang gánh | Mức tải | Rủi ro |
|:---|:---|:---|:---:|:---|
| **AI Product Owner / chủ bài toán** | Quyết định *khi nào được phép làm phiền người dùng* — quyết định sản phẩm, không phải kỹ thuật | Trang | Đủ | Thấp |
| **AI Engineer (Agent + RAG)** | Toàn bộ giá trị lõi nằm ở `fraud_intervention_agent` và kho 30 kịch bản | Bích | Đủ | Thấp |
| **Data / Backend Engineer** | Ví, giao dịch, JWT/RBAC, Alembic — không có thì agent không có gì để bảo vệ | Bích *(kiêm)* | **Quá tải** | Cao — 1 người ôm 2 vai |
| **Evals / Model QA** | Không có bộ đo thì mọi lời hứa với Compliance đều là ý kiến | Bích *(kiêm)* | **Quá tải** | **Rất cao** — người viết agent tự chấm agent |
| **UX cho người 32–55 tuổi** | Câu can thiệp viết sai giọng là người dùng bỏ qua, dù model đúng | Trang *(kiêm)* | Căng | Trung bình |
| **Domain Expert chống lừa đảo** | Kịch bản phải khớp thủ đoạn 2026, không phải thủ đoạn trong sách | **Không có in-house** — mượn ngoài | — | Cao |

**Kết luận đọc từ bảng:** team không thiếu *chức danh*, team thiếu **người thứ ba**. Hai vai đang chồng lên Bích (Backend + Evals) là điểm gãy gần nhất.

### 2.2. EXTENDED — chỉ cần khi scale, **cố ý chưa lập bây giờ**

| Vai trò | Kích hoạt khi nào | Vì sao chưa cần hôm nay |
|:---|:---|:---|
| MLOps / Observability | Khi có > 100 người dùng thật chạy hằng ngày | 20 tài khoản pilot còn xem log thủ công được |
| Legal / Compliance in-house | Khi chạm dữ liệu tài chính thật của khách hàng | Giai đoạn này mượn cố vấn theo giờ rẻ hơn nhiều |
| Forward Deployed Engineer | Khi có khách hàng doanh nghiệp hoặc ngân hàng tích hợp | Chưa có khách B2B nào |
| AI Ethics / Governance officer | Khi hệ thống tự động **chặn** giao dịch | VPay thiết kế human-in-the-loop — người dùng luôn giữ quyền quyết định cuối |
| Data Scientist riêng | Khi Risk Engine chuyển từ luật + Scikit-learn sang mô hình học sâu | Mô hình hiện tại phải chạy dưới 50ms, không cần deep learning |

> **Nguyên tắc team tự đặt:** không thêm chức danh nào mà không chỉ ra được **việc cụ thể trong 60 ngày tới** cho chức danh đó. 5 vai trên đều trượt bài kiểm tra này ở thời điểm hiện tại.

---

## 3. 🔧 Priority Resourcing — 3 capability gap quan trọng nhất (7')

### GAP 1 — Kiểm chứng tuân thủ & pháp lý dữ liệu tài chính → **PARTNER**

```
Capability gap : Không ai trong team đủ thẩm quyền nói "cách xử lý PII này là hợp lệ"
Cách bổ sung   : PARTNER — cố vấn BP An ninh & Compliance (nội bộ) + luật sư
                 fintech tư vấn theo giờ cho phần dữ liệu cá nhân
Vì sao         : Team đang tự viết whitepaper rồi tự thấy nó ổn — đúng kiểu
                 tự làm tự duyệt mà RACI hàng 1 đã cảnh báo. Cần một chữ ký
                 từ người ngoài. Tuyển full-time ở giai đoạn dữ liệu giả là
                 phí; outsource cũng không hợp vì cần người hiểu bối cảnh
                 nội bộ và dám ký.
Khi nào cần    : NGAY — trước buổi giải trình 04/09/2026, và bắt buộc phải
                 có trước khi pilot chạm dữ liệu người dùng thật
```

### GAP 2 — Sản xuất video FMV tương tác → **OUTSOURCE**

```
Capability gap : Viết kịch bản phân nhánh, quay, dựng, lồng tiếng video
                 tình huống lừa đảo — team không có ai làm được
Cách bổ sung   : OUTSOURCE — studio sản xuất video theo gói, team giữ
                 quyền viết kịch bản gốc và chốt nội dung từng nhánh
Vì sao         : Đây là năng lực dùng theo đợt, không lặp lại hằng tuần.
                 Tuyển người quay dựng full-time cho một module đang ở
                 trạng thái "Coming soon" là sai thứ tự ưu tiên. Chỉ thuê
                 phần sản xuất; phần quyết định nội dung nào đúng/sai
                 vẫn phải nằm trong team vì nó là domain chống lừa đảo.
Khi nào cần    : Từ 01/10/2026, sau khi pilot đóng xong vòng phản hồi
                 đầu tiên. Trước mốc đó, FMV giữ nguyên trạng thái
                 Coming soon trên UI, không hứa ngày phát hành.
```

### GAP 3 — Vận hành Evals & Observability liên tục → **HIRE (bán thời gian)**

```
Capability gap : Eval hiện chạy tay, kết quả nằm trong file JSON rời; không
                 có ai chạy lại tự động sau mỗi thay đổi, và người chấm
                 agent chính là người viết agent
Cách bổ sung   : HIRE — 1 cộng tác viên / thực tập sinh AI QA bán thời gian,
                 sở hữu bộ eval và pipeline chạy tự động trong CI
Vì sao         : Đây là việc lặp lại mỗi tuần và gắn chặt với codebase nên
                 outsource không hiệu quả — người ngoài mất quá nhiều thời
                 gian nạp bối cảnh cho một việc chạy đi chạy lại. Quan
                 trọng hơn: cần **người khác** cầm bộ đo để phá thế Bích
                 vừa viết agent vừa tự chấm agent, đúng rủi ro đã ghi ở
                 mục 2.1.
Khi nào cần    : Trước 25/09/2026 — mốc mở rộng bộ eval đối kháng từ
                 120 lên 300 lượt. Quá mốc này Bích không còn tải để ôm
                 cả Backend lẫn Evals.
```

### Gap đang được xử lý sẵn (không tính vào 3 ưu tiên)

| Capability gap | Cách bổ sung | Trạng thái |
|:---|:---|:---|
| Kịch bản lừa đảo cập nhật theo thủ đoạn 2026 | **PARTNER** — chuyên gia / cộng đồng anti-phishing | Đang chạy theo hành động A2 của Phase 1, hạn 11/09 |
| Webhook đối soát & tra cứu STK | **PARTNER** — SePay sandbox | Đã tích hợp, giữ nguyên |

### Tóm tắt quyết định

| Gap | Hire | Outsource | Partner | Mốc cần |
|:---|:---:|:---:|:---:|:---|
| Kiểm chứng tuân thủ & pháp lý PII | | | ✅ | 04/09/2026 |
| Sản xuất video FMV | | ✅ | | 01/10/2026 |
| Vận hành Evals & Observability | ✅ | | | 25/09/2026 |

---

## 4. 🎯 Squad Goal (5')

> **"Squad VPay sở hữu trọn vòng lặp Kiểm tra → Can thiệp → Luyện tập — gồm Cổng kép, `fraud_intervention_agent` và bộ eval của nó — và chịu trách nhiệm đưa cơ chế can thiệp chống lừa đảo từ trạng thái chạy trên dữ liệu mô phỏng, đến một pilot được BP An ninh & Compliance ký duyệt, có tỷ lệ làm phiền đo được trên máy người dùng thật dưới 20%."**

**Đọc câu này ra 3 cam kết kiểm chứng được:**

| Thành phần | Nội dung | Cách kiểm |
|:---|:---|:---|
| **Sở hữu cái gì** | Cổng kép + agent + bộ eval — cả phần chạy lẫn phần đo | Có repo, có 2 báo cáo eval, không phụ thuộc team khác |
| **Từ hiện trạng nào** | Dữ liệu mô phỏng, chưa có chữ ký duyệt, chưa có số liệu người dùng thật | Trạng thái ngày 29/08/2026 |
| **Đến đâu** | Pilot được ký duyệt + tỷ lệ làm phiền < 20% đo trên thiết bị thật | Văn bản duyệt của Compliance + số đo từ 5 ngày pilot (07–11/09) |

---

## 🚦 GATE 3 — Team Design phù hợp thực tế

- [x] Chọn **1 architecture duy nhất (Embedded)** và giải thích theo quy mô + giai đoạn thật, kèm điều kiện để đổi sang Hybrid
- [x] Đã sửa mâu thuẫn với tài liệu cũ (`PROJECT_OVERVIEW.md` ghi Hybrid)
- [x] Core Roles gắn với **người thật + mức tải + rủi ro**, chỉ rõ 2 vai đang chồng lên 1 người
- [x] Extended Roles nêu **điều kiện kích hoạt**, cố ý chưa lập — không chạy theo "càng nhiều chức danh càng tốt"
- [x] 3 capability gap, mỗi gap có đủ **Cách bổ sung → Vì sao → Khi nào cần**, và dùng cả 3 phương án Hire / Outsource / Partner
- [x] Lý do chọn phương án dựa trên **tần suất lặp lại của công việc và mức gắn với codebase**, không dựa trên chi phí chung chung
- [x] Squad Goal viết thành 1 câu, tách được thành 3 cam kết kiểm chứng

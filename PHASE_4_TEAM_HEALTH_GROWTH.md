# 📑 ARTEFACT 4 — TEAM HEALTH CHECK & 30-DAY GROWTH PLAN

> **Dự án:** VPay — Ví điện tử phòng chống lừa đảo chủ động bằng AI (`P-029`)
> **Team:** Lương Thanh Trang (Lead / Product Owner) · Đào Ngọc Bích (AI Engineer / QA)
> **Hình thức:** Cá nhân → Team · 25 phút
> **Ngày chấm:** 29/08/2026 · **Cửa sổ 30 ngày:** 29/08 → 28/09/2026

---

## 1. 🩺 Bước cá nhân — Tự chấm Team Health (5')

Bản nháp cá nhân của Bích tại [`2A202601745-DaoNgocBich/phase4_team_health_draft.md`](./2A202601745-DaoNgocBich/phase4_team_health_draft.md) để 3 dòng ở dạng `?` với ghi chú *"chỉ bạn và Trang biết"*. Bảng dưới giữ đúng tinh thần đó: **mỗi ô ghi rõ điểm dựa trên bằng chứng đo được hay còn là cảm nhận chờ xác nhận.**

| Khía cạnh | Trang | Bích | Cơ sở |
|:---|:---:|:---:|:---|
| **Chất lượng AI** | 4 | **3** | ✅ **Đo được.** Bích chấm thấp hơn vì đọc số theo lượt: recall@1 ở **lượt đầu chỉ 73.3%**. Trang chấm theo trải nghiệm tổng: recall@3 98.9%, 0 rò rỉ / 0 crash trong 120 lượt đối kháng |
| **Tiến độ** | 3 | 3 | ✅ **Đo được.** Nhịp commit đều, không ngày trống trong 14 ngày (7–61 commit/ngày, tổng 578). Nhưng cả 3 milestone Phase 0 đều **chưa đạt** → không chấm cao hơn 3 |
| **Tinh thần team** | 4 | 4 | ⚠️ **Cảm nhận — 2 thành viên phải xác nhận trước khi nộp.** Căn cứ gián tiếp: team tự nhận ra và tự sửa 3 lỗi tự đánh giá quá cao (milestone tick sai, số test sai, nhãn Hybrid sai) — dấu hiệu dám nói thật |
| **Tốc độ ra sản phẩm** | 3 | **2** | ✅ **Đo được.** `ci.yml` + `cd.yml` chạy lint + test + build trên mọi push nên thay đổi *code* ra nhanh. Nhưng **eval không nằm trong CI** — thay đổi *chất lượng agent* không có cổng nào chặn, phải chạy tay rồi đọc file JSON |

> ⚠️ **Phải làm trước khi nộp:** hai ô "Tinh thần team" là con số đề xuất, không phải kết quả tự chấm thật. Trang và Bích tự điền lại theo cảm nhận của mình. Nếu điểm thật lệch nhau ≥ 2, mục §2 phải viết lại.

---

## 2. 🔍 Bước team — So sánh điểm & chọn vấn đề (7')

### 2.1. Khía cạnh thấp nhất

**Tốc độ ra sản phẩm — trung bình 2.5/5**, thấp nhất trong 4 trục.

Nghịch lý: hạ tầng CI/CD đã có sẵn và chạy tốt, nhưng nó chỉ gác cổng **code không hỏng**, không gác cổng **agent không tệ đi**. Một thay đổi prompt hoặc ngưỡng risk engine có thể lên thẳng nhánh `develop` mà không bộ đo nào chặn lại.

### 2.2. Chênh lệch lớn nhất

| Trục | Trang | Bích | Lệch |
|:---|:---:|:---:|:---:|
| **Chất lượng AI** | 4 | 3 | **1** |
| **Tốc độ ra sản phẩm** | 3 | 2 | **1** |

**Vì sao lệch — cả hai lệch cùng một chiều và cùng một lý do:** Trang chấm theo **kết quả tổng hợp** (recall@3 98.9%, demo chạy mượt, deploy nhanh); Bích chấm theo **số xấu nhất trong báo cáo** (recall@1 lượt đầu 73.3%, eval nằm ngoài CI). Không phải bất đồng về sự thật — là khác nhau về **ngưỡng "đủ tốt"**.

**Cách team xử lý:** lấy góc nhìn của Bích làm chuẩn cho Growth Plan. Lý do: người trình bày với Compliance ngày 04/09 sẽ bị hỏi đúng con số xấu nhất, không ai hỏi con số đẹp nhất.

### 2.3. Vấn đề nếu không xử lý sẽ chặn milestone tiếp theo

> **Người viết agent cũng là người chấm agent, và bộ chấm chạy ngoài CI.**

Chuỗi hậu quả cụ thể:

```
Eval chạy tay, không gác cổng CI
   └─→ Thay đổi prompt / ngưỡng risk engine lên develop không ai chặn
        └─→ recall@1 lượt đầu (73.3%) có thể tụt tiếp mà không ai biết
             └─→ Pilot 5 user 07–11/09 gặp can thiệp sai ngay câu đầu
                  └─→ Tỷ lệ làm phiền vượt 20% → Squad Goal (Artefact 3) trượt
                       └─→ Compliance không có số liệu sạch để ký duyệt pilot
```

Vấn đề này đã bị chỉ ra 3 lần độc lập ở 3 artefact trước: rủi ro "tự làm–tự duyệt" (Artefact 2 §4.2), vai Evals chồng lên Bích (Artefact 3 §2.1), và capability gap 3 (Artefact 3 §3). **Đây là nút thắt duy nhất, không phải bốn vấn đề riêng lẻ.**

---

## 3. 📈 Bước team — Competency cần nâng cấp (5')

| Mục | Nội dung |
|:---|:---|
| **Role** | **AI Engineer** — Đào Ngọc Bích |
| **Level hiện tại** | **Gần L2 — AI Practitioner.** Đã build được agent chạy production: LangGraph `StateGraph`, RAG pgvector với RRF fusion, redact PII trong code path, tự viết và chạy 2 bộ eval. Chưa lên L3 vì bộ đo chưa vận hành tự động và chưa có người thứ hai kiểm chứng |
| **Competency cần nâng** | **Evals / quality evaluation** — chuyển từ *biết chạy eval* sang *vận hành eval như một cổng chất lượng bắt buộc* |
| **Action 30 ngày** | Xây bộ **30 golden case** (10 kịch bản × 3 lượt hội thoại) và đưa vào `ci.yml`, chạy tự động mỗi PR vào `develop`, **fail build** khi recall@3 < 95% hoặc số rò rỉ danh tính > 0 |

**Vì sao chọn đúng năng lực này:** đây là năng lực duy nhất vừa gỡ được nút thắt §2.3, vừa là điều kiện để Bích lên L3, vừa là bằng chứng Compliance cần thấy ngày 04/09. Ba mục tiêu, một hành động.

**Năng lực của Trang song song:** L1 → L2 ở mảng *stakeholder validation* — chuyển 8 stance giả định (Artefact 1 §2.3) thành stance có quan sát. Không tách thành action riêng vì đã nằm trong hành động 3 dưới đây.

---

## 4. 🗓️ Growth Plan 30 ngày (8') — 29/08 → 28/09/2026

| # | Vấn đề | Hành động 30 ngày | Owner | Deadline | Dấu hiệu hoàn thành |
|:---:|:---|:---|:---:|:---:|:---|
| **1** | Eval chạy tay, ngoài CI → thay đổi agent không có cổng chặn; người viết agent tự chấm agent | Thêm job `eval` vào `.github/workflows/ci.yml`: chạy bộ **30 golden case** mỗi PR vào `develop`, **fail build** khi recall@3 < 95% **hoặc** identity leak > 0. Kết quả đăng thành comment trên PR để Trang đọc được mà không cần mở JSON | **Bích** | **28/09/2026** | Có **≥ 1 PR thực sự bị CI chặn** vì eval fail, kèm link log. Không tính nếu job chỉ chạy mà chưa từng chặn ai |
| **2** | recall@1 lượt đầu **73.3%** — agent đoán sai kịch bản ngay câu đầu, đúng lúc người dùng dễ bỏ nhất | Nạp **≥ 5 kịch bản lừa đảo 2026** từ cộng đồng anti-phishing vào pgvector; tinh chỉnh truy vấn lượt 1 (mở rộng câu hỏi trước khi tìm vector). Mục tiêu **recall@1 lượt đầu ≥ 85%** | **Bích** | **25/09/2026** | File `reports/chat_agent-eval-<ngày>.json` mới, mục `by_turn."1".recall_at_1` **≥ 0.85**, đặt cạnh báo cáo 28/08 để so |
| **3** | 8/11 stance trong Stakeholder Map còn là giả định; 4/6 việc RACI gộp R = A nên không ai ngoài team kiểm | **Review 20 phút mỗi chiều thứ Sáu**, bắt đầu **04/09**. Mỗi buổi đóng **≥ 1 giả định** trong bảng Artefact 1 §2.3 (đổi ⚠️ Giả định → ✅ Đã quan sát, ghi nguồn), và ghi biên bản vào `JOURNAL.md` | **Trang** | **28/09/2026** | `JOURNAL.md` có **≥ 4 mục tuần** (05/09, 12/09, 19/09, 26/09); bảng §2.3 còn **≤ 4 giả định** vào 28/09 |

**Vì sao dừng ở 3 hành động:** team 2 người, mỗi người chỉ ôm được 1 việc cải tiến song song với việc chạy sản phẩm. Hành động 1 và 2 cùng Owner là Bích nhưng **không chồng nhau** — hành động 2 (25/09) đóng trước, hành động 1 (28/09) dùng chính bộ ca của hành động 2 làm golden case.

### Cách theo dõi

| Mốc | Kiểm gì |
|:---|:---|
| **05/09** | Buổi review thứ Sáu đầu tiên đã diễn ra chưa — nếu trượt buổi đầu, hành động 3 gần như chắc chắn chết |
| **11/09** | Số liệu pilot 5 user về, đối chiếu ngay với giả định "user thấy phiền" |
| **25/09** | recall@1 lượt đầu đã ≥ 0.85 chưa |
| **28/09** | Chấm lại đủ 4 trục Team Health, so với bảng §1 |

---

## 5. 📌 Ghi chú về phạm vi repo gốc — đã xác nhận

Rà `git log` của `P-029` cho thấy **6 tài khoản có commit**, tổng 578 commit tính đến 29/08/2026: `luongtrangba` (197), `nguyenthanhhoanwork-2508` (127), `Cuong` (122), `LewisDoo-01` (64), `Do Duc Cuong` (63), `Trang Luong` (4).

**Trang đã xác nhận:** `P-029` là **repository dùng chung của cohort**, có đóng góp từ người ngoài team Lab. Team Lab Day 27 vẫn đúng 2 người như khai ở Phase 0.

Hệ quả — giữ nguyên, không phải sửa:

| Kết luận ở artefact trước | Vẫn đúng vì |
|:---|:---|
| RACI gộp R = A ở 4/6 việc (Artefact 2 §4.2) | Người ngoài cohort không nhận trách nhiệm trong phạm vi Lab, nên không thể đứng tên R hoặc A |
| Bích ôm 4 vai, Evals quá tải (Artefact 3 §2.1) | Đúng trong phạm vi 2 người của team Lab |
| Gap 3 → **Hire** người vận hành Evals (Artefact 3 §3) | Vẫn cần: commit của người ngoài team không giải quyết được việc "cần người khác cầm bộ đo" |

Ghi chú này được đưa lên cả `README.md` Phase 0 để giám khảo mở `git log` không hiểu nhầm quy mô team.

---

## 🚦 GATE 4 — Growth Plan có thể thực thi

- [x] Chấm đủ **4 khía cạnh**, cả 2 thành viên, mỗi ô ghi rõ cơ sở là số đo hay cảm nhận
- [x] Chỉ ra khía cạnh thấp nhất (**Tốc độ ra sản phẩm — 2.5/5**) và giải thích nghịch lý CI có nhưng không gác chất lượng agent
- [x] Chỉ ra 2 điểm chênh lệch (đều lệch 1 điểm) và **lý do thật**: khác ngưỡng "đủ tốt", không phải bất đồng sự thật
- [x] Xác định **1 vấn đề chặn milestone**, vẽ được chuỗi hậu quả tới Squad Goal
- [x] Chọn **1 role · level hiện tại · 1 competency · 1 action 30 ngày** đúng khung L1/L2/L3
- [x] **3 hành động** (≤ 3), mỗi hành động đủ **Owner + Deadline + Dấu hiệu hoàn thành kiểm tra được**
- [x] Dấu hiệu hoàn thành là sự kiện quan sát được (PR bị chặn, số trong file JSON, số mục trong JOURNAL), không phải "team làm tốt hơn"
- [x] Đã xác nhận phạm vi repo gốc: `P-029` là repo chung cohort, team Lab vẫn 2 người — ghi chú ở §5 và README Phase 0
- [ ] ⚠️ **Chưa đóng:** 2 ô điểm "Tinh thần team" (§1) là con số đề xuất, cần Trang và Bích tự điền lại trước khi xuất PDF

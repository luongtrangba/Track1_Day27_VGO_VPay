# ✅ PHASE 5 — TỰ SOI LỖI CHÉO & NỘP BÀI

> **Dự án:** VPay — Ví điện tử phòng chống lừa đảo chủ động bằng AI (`P-029`)
> **Người phụ trách repo:** Lương Thanh Trang (trưởng nhóm) · **Ngày rà:** 30/08/2026
> **Câu hỏi trung tâm:** 4 artefact đã nhất quán và đủ bằng chứng chưa?

---

## 1. 🔗 Kiểm tra tính nhất quán giữa 4 artefact

Cách kiểm: mỗi con số và mỗi kết luận xuất hiện ở nhiều hơn một file đều được đối chiếu, không tin trí nhớ.

| Hạng mục | Giá trị chuẩn | Xuất hiện tại | Kết quả |
|:---|:---|:---|:---:|
| Số stakeholder | 11 (Trang 8 + Bích 7, trùng 4) | README · Artefact 1 · PROJECT_OVERVIEW | ✅ Khớp |
| Bộ test tự động | **1560 test** (`pytest --collect-only -q`) | README · Artefact 1 · Artefact 4 · PROJECT_OVERVIEW | ✅ Khớp |
| Eval chat agent 28/08 | 90 ca · recall@3 98.9% · recall@1 84.4% · p95 2.29s | README · Artefact 1 · Artefact 2 · PROJECT_OVERVIEW | ✅ Khớp |
| Eval đối kháng 27/08 | 120 lượt · 0 rò rỉ · 0 crash | README · Artefact 1 · Artefact 2 · Artefact 4 · PROJECT_OVERVIEW | ✅ Khớp |
| recall@1 lượt đầu | 73.3% (chỉ Artefact 4 dùng, đúng phạm vi) | Artefact 4 | ✅ Khớp |
| Mô hình tổ chức | **Embedded** | README · Artefact 3 · Artefact 4 | ✅ Khớp |
| Buổi giải trình Compliance | 04/09/2026 | Cả 4 artefact + PROJECT_OVERVIEW | ✅ Khớp |
| Mốc eval 120 → 300 lượt | 25/09/2026 | Artefact 2 · Artefact 3 · Artefact 4 | ✅ Khớp |

### 4 mâu thuẫn đã phát hiện và đã sửa

| # | Mâu thuẫn | Nằm ở đâu | Đã xử lý |
|:---:|:---|:---|:---|
| 1 | 3 milestone tick `[x]` như đã xong, trong đó có ">95% detection, <3% false-positive" chưa hề đo | README Phase 0 | Đổi về `[ ]`, ghi rõ là target; **cấm dùng 95%/3% làm evidence** trong Artefact 2 |
| 2 | "774+ tests · 12 eval cases" | README · PROJECT_OVERVIEW | Đếm thật: **1560 test** và 2 báo cáo eval JSON có sẵn (90 ca · 120 lượt) |
| 3 | Mô hình ghi là **Hybrid** | PROJECT_OVERVIEW mục 4 · README | Chốt lại **Embedded**, kèm điều kiện để đổi sang Hybrid (Artefact 3 §1) |
| 4 | Pitch nháp cũ hứa *"giảm 85% rủi ro mất tiền"* — không có nguồn | PROJECT_OVERVIEW mục 4 | Xoá; pitch chính thức chỉ dùng số đo từ 2 báo cáo eval trong repo |

> **Quy tắc ưu tiên khi còn mâu thuẫn:** `PROJECT_OVERVIEW.md` chỉ giữ vai trò bối cảnh (mục 1–3). Khi lệch nhau, **4 file artefact là chuẩn**.

---

## 2. 🧾 Kiểm tra đủ bằng chứng — không có con số nào không truy được nguồn

| Con số dùng trong bài | Nguồn kiểm chứng được |
|:---|:---|
| 0 rò rỉ danh tính · 0 lặp giá trị nhạy cảm · 0 crash / 120 lượt | `evals/agents/fraud_intervention_agent/reports/robustness-eval-20260827-024916.json` |
| recall@3 98.9% · recall@1 84.4% · MRR 0.916 · p95 2.29s / 90 ca | `.../reports/chat_agent-eval-20260828-173911.json` |
| recall@1 lượt đầu 73.3% | cùng file trên, mục `by_turn."1".recall_at_1` |
| 1560 test | `pytest --collect-only -q` trong `P-029` |
| Redact PII nằm trong code path | `src/agents/service/fraud_intervention_agent/chat_agent/security.py` |
| CI chạy lint + test + build trên mọi push | `.github/workflows/ci.yml`, `cd.yml` |
| 578 commit · 6 tài khoản · nhịp 7–61 commit/ngày | `git log` của `P-029` |
| `JOURNAL.md` chưa ghi tuần nào | file `JOURNAL.md` trong `P-029` |

**Không có con số nào trong 4 artefact thiếu nguồn.** Hai con số từng bị dùng sai (95% detection, 85% giảm rủi ro) đã bị loại bỏ hoàn toàn.

---

## 3. 🚦 Đối chiếu lại toàn bộ 5 gate

| Gate | Yêu cầu đề bài | Trạng thái |
|:---|:---|:---|
| **0** | Scope, thành viên, trưởng nhóm, format | ✅ 2 thành viên (team thật, ngoại lệ đã báo GV) · VPay `P-029` · Trang phụ trách repo · Google Docs → PDF ≤ 4 trang |
| **1** | ≥6 stakeholder cụ thể · map Influence × Interest · stance rõ · 4 hành động | ✅ 11 stakeholder · đủ 4 góc phần tư · stance kèm **cơ sở** (3 đã quan sát / 8 giả định có hạn kiểm chứng) · 4 hành động có người + số + hạn |
| **2** | Pitch kết luận trước + bằng chứng + small ask · 1 phản biện · RACI 4–6 việc mỗi việc 1 A | ✅ Pitch nhắm Compliance · bằng chứng từ 2 eval thật · small ask 45 phút ngày 04/09 · 1 phản biện + 3 hành động giảm rủi ro · RACI 6 việc, mỗi việc đúng 1 A |
| **3** | 1 architecture có giải thích · Core Roles · capability gap + Hire/Outsource/Partner | ✅ Embedded có lý do và điều kiện đổi · 6 Core Role gắn người thật + mức tải · 3 gap dùng đủ cả 3 phương án |
| **4** | Chấm 4 khía cạnh · chọn vấn đề · 1 competency · ≤3 hành động có owner + deadline | ✅ 4 trục đều neo vào dấu hiệu quan sát được · nút thắt vẽ được chuỗi hậu quả · AI Engineer gần L2 → nâng Evals · 3 hành động đủ Owner + Deadline + dấu hiệu |
| **5** | 4 artefact nhất quán · PDF ≤ 4 trang · repo hoàn chỉnh | ✅ 4 mâu thuẫn đã sửa · **PDF đúng 4 trang A4** · repo có README + 4 file artefact + thư mục cá nhân |

---

## 4. 📦 Bài nộp

| Thành phần | File | Ghi chú |
|:---|:---|:---|
| Trang bìa & Phase 0 | [`README.md`](./README.md) | Thành viên, scope, milestone (trạng thái thật), bằng chứng, gate check |
| **Bản nộp chính** | [`Day27_VGO_VPay.pdf`](./Day27_VGO_VPay.pdf) | **4 trang A4**, mỗi trang một artefact |
| Artefact 1 | [`PHASE_1_STAKEHOLDER_MAP.md`](./PHASE_1_STAKEHOLDER_MAP.md) | Bản nguồn chi tiết |
| Artefact 2 | [`PHASE_2_PITCH_RACI.md`](./PHASE_2_PITCH_RACI.md) | Bản nguồn chi tiết |
| Artefact 3 | [`PHASE_3_AI_TEAM_DESIGN.md`](./PHASE_3_AI_TEAM_DESIGN.md) | Bản nguồn chi tiết |
| Artefact 4 | [`PHASE_4_TEAM_HEALTH_GROWTH.md`](./PHASE_4_TEAM_HEALTH_GROWTH.md) | Bản nguồn chi tiết |
| Bối cảnh dự án | [`PROJECT_OVERVIEW.md`](./PROJECT_OVERVIEW.md) | Mục 1–3 là bối cảnh; mục 4 trỏ về 4 artefact |
| Bước cá nhân của Bích | [`2A202601745-DaoNgocBich/`](./2A202601745-DaoNgocBich/) | Giữ nguyên bản gốc để đối chiếu bước "Cá nhân → Team" |

**Việc cuối của trưởng nhóm trước khi nộp:** commit toàn bộ thay đổi, đẩy lên GitHub, **đặt repository ở chế độ public**, rồi nộp link repository.

---

## 🚦 GATE 5 — Sẵn sàng nộp

- [x] Rà chéo 8 hạng mục số liệu dùng ở nhiều file — tất cả khớp
- [x] Phát hiện và sửa **4 mâu thuẫn** giữa bản nháp sớm và kết quả cuối
- [x] Mọi con số trong bài đều truy được về một file cụ thể trong `P-029`
- [x] Loại bỏ hoàn toàn 2 con số từng dùng sai (95% detection · 85% giảm rủi ro)
- [x] Đối chiếu lại đủ 5 gate của đề bài
- [x] **PDF đúng 4 trang A4**, tiếng Việt hiển thị đủ dấu
- [ ] Trưởng nhóm commit, push và **đặt repo ở chế độ public** trước khi nộp link

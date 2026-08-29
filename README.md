# 🚀 Day 27 — AI Team Lab: Từ Stakeholder đến Team Health & Growth Plan

> **Chương trình:** AI Product Development & Engineering Lab  
> **Track:** Track 1  
> **Tên Team:** VGO / VPay Team  
> **Mã Team:** Team VGO (Track 1)  
> **Tên Dự Án:** **VPay** — Ví điện tử mô phỏng phòng chống lừa đảo chủ động bằng AI (Proactive Anti-Fraud E-Wallet)  
> **Base Repository:** `D:\AITHUCCHIEN\BUILD-PHASE-1\P-029`

---

## 👥 Danh Sách Thành Viên (Team Members)

| STT | Họ và Tên | Role trong Team | Trách nhiệm chính trong Lab | Ghi chú |
|:---:|:---|:---|:---|:---|
| 1 | **Lương Thanh Trang** | Product Owner / AI Lead | Quản lý Stakeholder, Pitch, Quản lý Repository & Điều phối chung | Trưởng nhóm / Accountable |
| 2 | **Đào Ngọc Bích** | AI Engineer / Fullstack & QA | Thiết kế AI Team Architecture, RACI Matrix, Team Health & Growth Plan | Đồng phụ trách / Responsible |

> ⚠️ **Quy mô team — 2 người, đã báo giảng viên.** Đề bài yêu cầu 3–5 thành viên. Team VGO chỉ có 2 người và đây là **team dự án cố định có thật**, không phải team lập riêng để làm Lab. Áp dụng đúng ngoại lệ đề bài cho phép: *"Nếu lớp đã có team dự án cố định khác quy mô này, giữ nguyên team hiện tại và báo giảng viên trước khi bắt đầu Lab."*
> Hệ quả kéo theo đã được xử lý trong bài, không né tránh: RACI chỉ tách được R ≠ A ở 2/6 công việc — 4 việc còn lại gộp R = A và mỗi việc đều gắn 1 người ngoài team làm **C bắt buộc** để chặn tự làm–tự duyệt (xem [Artefact 2](./PHASE_2_PITCH_RACI.md) §4.2).

> 📌 **Về repo gốc `P-029`:** đây là **repository dùng chung của cohort**, có commit từ nhiều tài khoản ngoài team Lab (6 tài khoản / 578 commit tính đến 29/08/2026). Team Lab Day 27 vẫn là 2 người như bảng trên; toàn bộ 4 artefact chỉ đánh giá phạm vi công việc của 2 thành viên này, không tính phần đóng góp của người ngoài team.

**Thư mục làm việc cá nhân:** [`2A202601745-DaoNgocBich/`](./2A202601745-DaoNgocBich/) — bản nháp cá nhân bước "Cá nhân" của Bích ở Phase 0, 1, 4. Các bản nháp này được gộp vào artefact chung ở bước "Team", giữ nguyên file gốc để đối chiếu.

---

## 📌 Phase 0 — Chốt Phạm Vi & Mục Tiêu Dự Án (Scope & Goal)

* **Bối cảnh & Vấn đề (Context & Problem):** 
  Hơn 90% nạn nhân tự tay chuyển tiền cho kẻ lừa đảo do bị thao túng tâm lý (social engineering), không phải do bị hack tài khoản. Các cảnh báo chung chung bị phớt lờ và thiếu phản xạ thực tế.
* **Giải pháp đề xuất (Proposed Solution):** 
  Hệ thống ví điện tử mô phỏng theo cơ chế vòng lặp **Kiểm tra → Can thiệp → Luyện tập** với:
  - **Cổng kép (Dual Gate):** Mô hình chấm điểm rủi ro hành vi (Scikit-Learn + Luật tĩnh) kết hợp cùng AI Agent phản biện (`fraud_intervention_agent` qua LangGraph + RAG pgvector).
  - **Human-in-the-loop & Trusted Contact:** Không tự ý chặn cứng mà đặt câu hỏi làm rõ để người dùng tự quyết định, đồng thời gửi cảnh báo tối thiểu đến người thân tin cậy.
  - **Game phản xạ FMV:** Mô phỏng tình huống lừa đảo thật để rèn luyện phản xạ phòng ngừa.
* **Mục tiêu 1–3 tháng tới (Key Milestones) — đều là *target chưa đạt*, không phải việc đã xong:**
  - [ ] Tối ưu `fraud_intervention_agent`: tỷ lệ phát hiện gian lận > 95%, false-positive < 3%. ⚠️ **Chưa đo được** — hai con số này là mục tiêu, chưa có báo cáo eval nào chứng minh.
  - [ ] Hoàn thiện game tương tác FMV và hệ thống cảnh báo Người tin cậy (Trusted Contact). FMV hiện ở trạng thái **Coming soon**, chưa chốt ngày phát hành.
  - [ ] Chuẩn hóa Agentic Workflow giữa Human & AI, nâng năng lực AI của team từ L1 lên L2/L3.

> 🔎 **Ghi chú trung thực về số liệu (chốt ở Phase 0, ràng buộc toàn bộ Lab).**
> Ba milestone trên là *đích đến*, không phải bằng chứng. Theo luật Lab — *"Pitch dùng Conclusion First nhưng không được hứa vượt quá bằng chứng hiện có"* — con số **95% / 3% bị cấm dùng làm evidence** trong Artefact 2.
> Bằng chứng thật sự đang có, đã kiểm trong repo `P-029` ngày 29/08/2026:
> | Bằng chứng | Số đo thật | Nguồn |
> |:---|:---|:---|
> | Bộ eval chat agent (28/08/2026) | 90 ca · recall@3 **98.9%** · recall@1 84.4% · MRR 0.916 · đạt ngưỡng 96.7% · độ trễ p95 **2.29s** | `evals/agents/fraud_intervention_agent/reports/chat_agent-eval-20260828-173911.json` |
> | Bộ eval đối kháng (27/08/2026) | 120 lượt · 10 nhóm · **0 rò rỉ danh tính, 0 lặp giá trị nhạy cảm, 0 crash** | `.../reports/robustness-eval-20260827-024916.json` |
> | Bộ test tự động | **1560 test** thu thập được bằng `pytest --collect-only -q` | repo `P-029` |
>
> Con số "774+ tests / 12 eval cases" ở các bản tài liệu trước là **ước lượng sai**, đã thay bằng số đếm thật ở bảng trên.

* **Format làm bài:** Google Docs / Google Slides để soạn nội dung 4 artefact → export thành **01 file PDF ≤ 4 trang** nộp kèm repo. Bản nguồn của từng artefact được giữ dưới dạng file Markdown trong repo này để chấm chi tiết.

---

## 📑 Cấu Trúc Báo Cáo Nộp Bài (4 Artefacts / 4-Page Report)

File báo cáo chính thức: [Day27_AI-Team-Lab_TeamXX.pdf](./Day27_AI-Team-Lab_TeamXX.pdf)

Báo cáo gồm 4 trang tiêu chuẩn tương ứng với 4 Artefact:
1. **Trang 1 (Artefact 1) — Stakeholder Map & 4 Chiến Lược Tương Tác:**
   - Phân loại Stakeholder theo ma trận *Influence × Interest* (Champion, Blocker, Supporter, Bystander) và Stance thực tế.
   - Chiến lược tương tác và giải quyết lo ngại cho từng nhóm bên liên quan.
2. **Trang 2 (Artefact 2) — 60s Elevator Pitch (Conclusion First) & RACI Matrix:**
   - Bài thuyết phục 60 giây theo cấu trúc *Conclusion First* dựa trên số liệu và bằng chứng thực tế của VPay.
   - Bảng phân định trách nhiệm RACI rõ ràng, độc lập vai trò Responsible (R) và Accountable (A).
3. **Trang 3 (Artefact 3) — AI Team Architecture & Priority Resourcing:**
   - Cấu trúc tổ chức AI Team: chốt **Embedded** (không phải Hybrid — xem lý do trong Artefact 3), danh mục Core Roles gắn người thật và mức tải.
   - Phân tích Capability Gaps và chiến lược bù đắp năng lực: *Hire / Outsource / Partner*.
4. **Trang 4 (Artefact 4) — Team Health Check & 30-Day Continuous Growth Plan:**
   - Đánh giá sức khỏe đội ngũ qua 4 khía cạnh (Chất lượng AI, Tiến độ, Tinh thần, Tốc độ).
   - Kế hoạch hành động 30 ngày chi tiết (*Action + Owner + Deadline + Metric*).

---

## 🛠️ Công Nghệ & AI Tooling của VPay (Tech Stack)

- **AI Agent Framework:** LangGraph (`StateGraph`), LangChain (`langchain-openai`), OpenRouter (`gemini-2.5-flash`).
- **RAG & Vector Database:** Neon PostgreSQL + pgvector, embedding `multilingual-e5-large` (1024d), RRF fusion search.
- **Backend & Risk Engine:** FastAPI, Python 3.13, Scikit-learn, Pandas, SQLAlchemy 2.0 + Alembic.
- **Client & Frontend:** React Native (Expo SDK 57), React + Vite (Admin Console & Landing Page).
- **Testing & Evals:** 1560 test thu thập bằng `pytest --collect-only -q`; 2 bộ eval đã chạy có báo cáo JSON (90 ca chat agent, 120 lượt đối kháng) trong `evals/agents/fraud_intervention_agent/reports/`.

---

## 🚦 Gate Check Status

- [x] **GATE 0 — Scope đã rõ:** Chốt 2 thành viên (team thật, đã báo GV), dự án VPay (`P-029`), trưởng nhóm Lương Thanh Trang, format Google Docs → PDF ≤ 4 trang, và **chốt trạng thái thật của 3 milestone** (target chưa đạt, cấm dùng 95%/3% làm evidence).
- [x] **GATE 1 — Stakeholder Map:** Gộp 2 danh sách cá nhân (Trang 8 + Bích 7) → 11 stakeholder, đủ 4 góc phần tư, stance có ghi rõ cơ sở (3 đã quan sát / 8 giả định kèm kế hoạch kiểm chứng), 4 hành động ưu tiên kèm deadline → [PHASE_1_STAKEHOLDER_MAP.md](./PHASE_1_STAKEHOLDER_MAP.md).
- [x] **GATE 2 — Pitch & RACI:** Pitch Conclusion First dựa trên 2 báo cáo eval thật, có phản biện + 3 hành động giảm rủi ro, RACI 6 việc mỗi việc đúng 1 Accountable → [PHASE_2_PITCH_RACI.md](./PHASE_2_PITCH_RACI.md).
- [x] **GATE 3 — AI Team Design:** Chốt mô hình Embedded (sửa lại từ Hybrid), 6 Core Role gắn người thật, 3 capability gap dùng đủ Partner/Outsource/Hire → [PHASE_3_AI_TEAM_DESIGN.md](./PHASE_3_AI_TEAM_DESIGN.md).
- [x] **GATE 4 — Team Health & Growth:** Chấm đủ 4 trục (thấp nhất: Tốc độ ra sản phẩm 2.5/5), chốt 1 nút thắt chặn milestone, nâng competency Evals của AI Engineer lên L3, 3 hành động 30 ngày có Owner + Deadline + dấu hiệu hoàn thành → [PHASE_4_TEAM_HEALTH_GROWTH.md](./PHASE_4_TEAM_HEALTH_GROWTH.md). ⚠️ Còn 1 mục chờ: 2 ô điểm "Tinh thần team" cần 2 thành viên tự điền (§1).
- [ ] **GATE 5 — Nộp bài:** File PDF $\le$ 4 trang và repo public.
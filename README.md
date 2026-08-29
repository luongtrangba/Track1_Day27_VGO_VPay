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

---

## 📌 Phase 0 — Chốt Phạm Vi & Mục Tiêu Dự Án (Scope & Goal)

* **Bối cảnh & Vấn đề (Context & Problem):** 
  Hơn 90% nạn nhân tự tay chuyển tiền cho kẻ lừa đảo do bị thao túng tâm lý (social engineering), không phải do bị hack tài khoản. Các cảnh báo chung chung bị phớt lờ và thiếu phản xạ thực tế.
* **Giải pháp đề xuất (Proposed Solution):** 
  Hệ thống ví điện tử mô phỏng theo cơ chế vòng lặp **Kiểm tra → Can thiệp → Luyện tập** với:
  - **Cổng kép (Dual Gate):** Mô hình chấm điểm rủi ro hành vi (Scikit-Learn + Luật tĩnh) kết hợp cùng AI Agent phản biện (`fraud_intervention_agent` qua LangGraph + RAG pgvector).
  - **Human-in-the-loop & Trusted Contact:** Không tự ý chặn cứng mà đặt câu hỏi làm rõ để người dùng tự quyết định, đồng thời gửi cảnh báo tối thiểu đến người thân tin cậy.
  - **Game phản xạ FMV:** Mô phỏng tình huống lừa đảo thật để rèn luyện phản xạ phòng ngừa.
* **Mục tiêu 1–3 tháng tới (Key Milestones):**
  - [x] Triển khai và tối ưu hóa hệ thống `fraud_intervention_agent` với tỷ lệ phát hiện gian lận > 95%, giảm false-positive xuống dưới 3%.
  - [x] Hoàn thiện tích hợp game tương tác FMV và hệ thống cảnh báo Người tin cậy (Trusted Contact).
  - [x] Chuẩn hóa quy trình làm việc giữa Human & AI Agents (Agentic Workflow), nâng cao Team Health & chỉ số trưởng thành năng lực AI L1 $\rightarrow$ L2/L3.

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
   - Cấu trúc tổ chức AI Team (Embedded / Hybrid), danh mục Core Roles hiện tại.
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
- **Testing & Evals:** 774+ tests (`pytest`), 12 eval cases (`evals/`).

---

## 🚦 Gate Check Status

- [x] **GATE 0 — Scope đã rõ:** Đã chốt thành viên (Lương Thanh Trang, Đào Ngọc Bích), dự án VPay (`P-029`), vai trò và repository nộp bài.
- [x] **GATE 1 — Stakeholder Map:** 11 stakeholder cụ thể, đủ 4 góc phần tư, có stance thực tế và 4 hành động ưu tiên kèm deadline → [PHASE_1_STAKEHOLDER_MAP.md](./PHASE_1_STAKEHOLDER_MAP.md).
- [ ] **GATE 2 — Pitch & RACI:** Pitch Conclusion First có bằng chứng, RACI có duy nhất 1 Accountable/nhiệm vụ.
- [ ] **GATE 3 — AI Team Design:** Cấu trúc team phù hợp quy mô, giải thích rõ Hire/Outsource/Partner.
- [ ] **GATE 4 — Team Health & Growth:** Growth plan có Action + Owner + Deadline khả thi.
- [ ] **GATE 5 — Nộp bài:** File PDF $\le$ 4 trang và repo public.
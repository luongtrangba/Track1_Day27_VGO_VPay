# Phase 0 — Chốt phạm vi & cách làm (Draft cá nhân — cần sync với team)

> File này là bản đề xuất cá nhân của Đào Ngọc Bích, dùng để mang vào buổi sync
> Phase 0 với Lương Thanh Trang. Sau khi team thống nhất, Trang (trưởng nhóm)
> cập nhật bản chính thức vào `README.md` ở gốc repo.

## 1. Thành viên team
- Lương Thanh Trang — Product Owner / AI Lead (Accountable, quản lý repo & điều phối)
- Đào Ngọc Bích — AI Engineer / Fullstack & QA (Responsible kỹ thuật)

✅ **Đã xác nhận**: team cố định 2 người (Trang + Bích) là toàn bộ team Track 1
thực tế, không phải team giả lập cho Lab — đúng trường hợp ngoại lệ đề bài cho
phép. Cần ghi rõ điều này vào README để GV không thắc mắc khi chấm.

## 2. Tên dự án
**VPay** — Ví điện tử phòng chống lừa đảo chủ động bằng AI
(hệ sinh thái VGO, dự án gốc `P-029`)

## 3. Mục tiêu hiện tại (1–3 tháng tới)
✅ **Đã xác nhận**: cả 3 milestone đều là **ước lượng/target, chưa đo thật**.
README đang tick `[x]` là sai trạng thái — cần sửa lại thành `[ ]` (chưa đạt,
đang hướng tới):

- [ ] Tối ưu `fraud_intervention_agent`: tỷ lệ phát hiện gian lận > 95%,
      false-positive < 3% *(target, chưa có eval report thật)*
- [ ] Hoàn thiện tích hợp game FMV + hệ thống cảnh báo Trusted Contact
- [ ] Chuẩn hóa Agentic Workflow giữa Human & AI, nâng Team Health & năng lực
      AI từ L1 → L2/L3

⚠️ **Hệ quả quan trọng cho Artefact 2 (Pitch)**: vì 95%/3% chưa có số đo thật,
**không được dùng con số này làm bằng chứng (evidence)** trong Pitch — vi phạm
thẳng luật "Conclusion First nhưng không hứa vượt bằng chứng hiện có". Khi làm
Pitch, phải tìm bằng chứng khác đang thực sự có (vd: kiến trúc đã build xong,
774+ test pass, 12 eval case đã chạy — nếu có kết quả) thay vì số liệu
detection rate chưa đo.

## 4. Trưởng nhóm / người tổng hợp
**Lương Thanh Trang** — tạo repository, đảm bảo artefact chung được cập nhật
đầy đủ (theo README hiện tại, vai trò PO/AI Lead — Accountable).

## 5. Format làm bài
Vẫn đề xuất: Google Docs/Slides để draft nội dung 4 artefact, sau đó export
thành 1 file PDF ≤ 4 trang theo yêu cầu nộp bài (mục 10 của đề bài) — cần
Trang xác nhận vì đây là quyết định chung của team.

---

## Việc cần làm trước khi qua Gate 0
1. ✅ Xác nhận team 2 người là thật, không phải giả lập.
2. ✅ Xác nhận 3 milestone đều là target chưa đo.
3. Chốt format làm bài (Docs/Slides/FigJam/Miro) với Trang.
4. Trang cập nhật `README.md` gốc: sửa milestone `[x]` → `[ ]`, ghi chú lý do
   team chỉ 2 người, tick Gate 0.

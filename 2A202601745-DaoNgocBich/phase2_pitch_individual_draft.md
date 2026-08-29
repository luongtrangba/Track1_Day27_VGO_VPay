# Phase 2 — Bước cá nhân: Pitch viết lại (nháp thật, chờ Bích đọc & chỉnh giọng văn)

> Đây là bước cá nhân THẬT — khác với bản "Bản của Đào Ngọc Bích" mà Trang đã
> tự viết hộ trước đó (đang được Trang gỡ/sửa). Bản dưới đây viết dựa trên
> Pitch nháp thật của Team (mục 1.2, `PHASE_2_PITCH_RACI.md`), theo góc nhìn
> **QA — quy trình kiểm thử & khả năng tái lập**, cố ý khác hướng "ranh giới
> dữ liệu trong code" mà bản cũ dùng, để tránh trùng góc nhìn.

## Bản nháp (đọc, sửa lại câu chữ cho đúng giọng của bạn)

> **Kết luận.** Em đề nghị duyệt pilot giới hạn: 20 tài khoản nội bộ, dữ liệu
> giả, 2 tuần.
>
> **Lý do.** Với vai trò QA, cái em quan tâm nhất không phải là "AI có tốt
> không" mà là "nếu AI sai, mình có phát hiện được không, và phát hiện bao
> nhanh". Hai báo cáo eval của team không phải chạy một lần rồi thôi — chúng
> là quy trình có thể chạy lại bất cứ lúc nào, với bộ ca kiểm thử lưu sẵn
> trong repo, kết quả ra JSON đọc được từng dòng. Nghĩa là nếu anh/chị nghi
> ngờ một con số, em chạy lại ngay trước mặt anh/chị được, không phải "tin
> vào lời team nói".
>
> **Bằng chứng.** Báo cáo 27/08: 120 lượt kiểm thử đối kháng (18 jailbreak,
> 11 lượt đòi dữ liệu nhạy cảm, 8 lượt dò danh tính hệ thống) — 0 lượt rò rỉ,
> 0 lượt lặp giá trị nhạy cảm, 0 crash. Báo cáo 28/08: 90 ca trên 30 kịch bản
> × 3 lượt, recall@3 98.9%, độ trễ p95 2.29 giây. Cả hai bộ test đều là test
> **đối kháng có chủ đích** — không phải test ngẫu nhiên dễ đạt điểm cao.
>
> **Small ask.** Cho em 45 phút ngày 04/09 để mở trực tiếp 2 file JSON kết
> quả, chạy lại 1 ca bất kỳ anh/chị chọn ngay tại chỗ. Nếu ca đó không khớp
> với báo cáo, team dừng pilot và sửa trước khi xin lại.

## Việc bạn cần làm để hoàn tất
1. Đọc lại, sửa câu chữ cho đúng giọng văn thật của bạn — đây chỉ là khung ý,
   không phải bản để copy nguyên.
2. Xác nhận với chính mình: góc "khả năng tái lập kết quả eval" có đúng là
   điều bạn thực sự quan tâm nhất với vai trò QA không, hay bạn muốn nhấn vào
   khía cạnh khác (vd độ phủ test case, quy trình CI)?
3. Khi Trang sửa xong Phase 1, mang bản này thay cho bản cũ ở mục 3.2 của
   `PHASE_2_PITCH_RACI.md`.

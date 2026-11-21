# Exit ticket — Ngày 12

Làm cá nhân, không mở slide, khoảng 10 phút. Ghi đáp án ngay dưới mỗi câu.

**Họ tên:** Phạm Văn Hùng · **Mã:** G04



---

**Câu 1 · Chọn một.** Camera DMS trên nhiều xe tự chiếu đèn LED cận hồng ngoại khoảng 940 nm lên mặt tài xế. Lý do chính là gì?

- A. Để đo nhiệt độ da và phát hiện tài xế bị sốt
- B. Để có ảnh mặt ổn định cả ngày lẫn đêm mà không làm chói mắt tài xế
- C. Để có ảnh màu đẹp hơn cho cuộc gọi video
- D. Để camera nhìn xuyên qua mọi loại kính râm

Đáp án: **B**

Giải thích ngắn: 940 nm là cận hồng ngoại, mắt người gần như không thấy nên không gây chói, còn camera vẫn thu được ảnh ổn định cả đêm lẫn khi ngược sáng (như ảnh D01–D06). A sai vì đo nhiệt cần camera nhiệt (hồng ngoại xa); C sai vì ảnh NIR là ảnh đơn sắc; D sai vì NIR chỉ xuyên được một số loại kính râm, không phải mọi loại.

**Câu 2 · Số, 2 chữ số thập phân.** Camera DMS chạy 30 khung hình/giây. Model ước lượng yaw của đầu tài xế lớn hơn 30° liên tục từ khung hình số 240 đến khung hình số 314, **tính cả khung 240 và khung 314**. Tài xế không nhìn đường trong bao nhiêu giây?

Đáp án: **2.50** s

Cách tính: số khung = 314 − 240 + 1 = 75 khung; 75 / 30 = 2.50 s.

**Câu 3 · Chọn tất cả đáp án đúng.** Những câu nào đúng về dữ liệu cabin so với dữ liệu camera ngoài xe?

- A. Không thể làm mờ mặt tài xế như làm mờ mặt người qua đường, vì model DMS cần chính khuôn mặt.
- B. Ban đêm, ảnh cabin thường là ảnh hồng ngoại đen trắng, nên thuộc tính màu áo không gán được.
- C. Camera OMS nhìn về phía sau xe, nên ghế ở bên trái ảnh là ghế bên phải của xe.
- D. Vật trong cabin thường ở xa và nhỏ, nhiều vật trong một ảnh.
- E. Cảnh cabin cố định nên không cần guideline hay QC riêng.

Đáp án: **A, B, C**

Giải thích ngắn: A đúng vì DMS cần mắt, mặt để đọc trạng thái; B đúng vì ảnh IR mất màu (ir_log dòng S01_ir); C đúng (quy tắc ghế theo xe, GUIDE 4.4-3). D sai vì vật trong cabin ở gần camera và thường lớn trong khung hình; E sai vì hôm nay vẫn phát sinh nhiều lỗi (ghế lật, trái/phải mắt, cờ occluded) phải bắt bằng guideline, `cabin_check` và review chéo.

# Tự đánh giá — Phạm Văn Hùng · G04

## 1. Tự rà soát 4 cảnh

| Ảnh | Đối tượng | Loại lỗi | Ghi chú | Đã sửa? |
|---|---|---|---|---|
| S01_rgb | child_seat rear_right | wrong_class (giá trị) | Ghế có trẻ ngồi ghi `occupied = yes`, guideline v1.0 không có giá trị này, `cabin_check` báo ERROR | Có, đổi sang `unknown` |
| S08_rgb | person rear_right | ok | RGB tối, không thấy ngực nên `seatbelt = unknown`, không chép `not_worn` từ ảnh IR | — |
| D02 | face13 | flag | Bật `occluded` cho 12/13 điểm dù mắt nhìn thấy qua kính trong | Có, tắt `occluded` cho điểm nhìn thấy |
| D06 | face13, hand | missing | Thiếu skeleton `face13` (mặt > 60 px) và thiếu box tay phải phía trên | Có, đã vẽ bổ sung |

## 2. Lỗi mình lặp lại nhiều nhất hôm nay

Lỗi: dùng cờ `occluded` sai: bật cho cả những điểm nhìn thấy được (D02, D05), và dùng `occluded` cho điểm không đoán được vị trí lẽ ra phải là `outside` (D03). Ở D05 còn mâu thuẫn: mắt ghi `open` nhưng cả 8 điểm mắt `occluded`, `cabin_check` cảnh báo.

Vì sao mình mắc: thấy ảnh NIR tối và có kính nên nghĩ "bị che" cho an toàn, chưa phân biệt rõ ba trường hợp: thấy được / bị che nhưng đoán chắc / không đoán được.

Lần sau tránh bằng cách: với mỗi điểm hỏi 2 câu: "mình có thấy điểm này không?" (thấy → để bình thường); nếu không thấy: "mình có chắc vị trí không?" (chắc → `occluded`, không → `outside`). Sau khi vẽ xong, so cờ điểm mắt với thuộc tính `eye_left`/`eye_right` để không mâu thuẫn.

Lỗi thứ hai: quên tag `frame_meta` ở D04–D06. Lần sau đặt tag ngay khi mở ảnh, trước box đầu tiên.

## 3. Ghi chú về disagreement_log

Một dòng bạn của mình đúng và mình sai: **S02 (rgb và ir), object ở rear_middle**. Mình vẽ box `object` cho một vật nhỏ tối ở khe ghế giữa, nhưng đó thực ra là khóa dây an toàn của xe (xuất hiện ở cùng vị trí trên mọi cảnh). Bạn không gán và đúng theo GUIDE 4.2 (không gán bộ phận của xe). Đã xóa trong `export_final_v2.zip`.

Mình học được gì từ dòng đó: trước khi gán `object`, so cùng vị trí trên các cảnh khác; vật lặp lại ở đúng chỗ trên mọi ảnh thường là một phần của xe, không phải đồ mang theo.

Dòng thứ hai bạn đúng: **D03 seatbelt**. Mình để `unknown`, nhưng phóng to thì thấy rõ dải dây trên ngực → `worn_correct` (GUIDE 4.7). Đã sửa trong v2.

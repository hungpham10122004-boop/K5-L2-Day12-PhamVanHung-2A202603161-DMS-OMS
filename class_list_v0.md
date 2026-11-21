# Danh sách lớp v0 — Phạm Văn Hùng · G04

Viết tiếp từ slide 54 bài giảng. Mỗi lớp trả lời: **model cần nhận ra cái này để làm gì?**

## DMS (8 lớp)

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng DMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | eye_state (eye_left, eye_right) | open / closed / unknown | Phát hiện buồn ngủ: mắt nhắm kéo dài nhiều khung (PERCLOS) | Có, trừ khi đốm phản xạ LED trên kính hoặc mặt quay đi (D01, D03) |
| 2 | gaze_zone | road / mirror_l / mirror_r / mirror_c / cluster / center / lap / other | Phát hiện mất tập trung: rời mắt khỏi đường quá ngưỡng thời gian | Một phần: hướng đầu thấy rõ, hướng mắt khó khi mặt quay (D01) |
| 3 | head_pose (yaw / pitch) | góc liên tục | Bổ trợ gaze khi không thấy mắt; cảnh báo quay đầu lâu | Có (hình dạng đầu, mũi, tai) |
| 4 | glasses | none / clear / sun / unknown | Biết khi nào kết quả eye_state kém tin cậy; chọn cách xử lý phản xạ | Thấy gọng; khó phân biệt clear/sun vì NIR xuyên kính râm (D06) |
| 5 | hand.on_wheel | yes / no / unknown | Cảnh báo buông vô lăng (hands-off) khi xe không ở chế độ tự lái | Có, nếu tay nằm trong khung hình |
| 6 | phone | held / mounted / lap | Phát hiện dùng điện thoại khi lái (nhắn tin, gọi) | Thấy hình dạng; màn hình sáng không giúp trên NIR |
| 7 | eating_drinking (vật trên tay gần miệng) | có / không | Phân biệt phân tâm do ăn uống với điện thoại, tránh báo nhầm phone (D05 chai nước) | Có (hình dạng chai/cốc) |
| 8 | seatbelt (tài xế) | worn_correct / worn_incorrect / not_worn / unknown | Nhắc thắt dây an toàn, phát hiện thắt sai (dưới nách) | Có, dải dây tối trên áo sáng (D01, D06) |

## OMS (7 lớp)

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng OMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | person + seat | theo 5 ghế | Đếm người, nhắc thắt dây theo từng ghế, điều chỉnh điều hòa/âm thanh theo vùng | Có |
| 2 | seatbelt (hành khách) | worn_correct / worn_incorrect / not_worn / unknown | Cảnh báo hành khách chưa thắt dây | Có; trên RGB tối thì không (S08) |
| 3 | child_seat + occupied | no / unknown (v1.x đề xuất thêm yes) | Tắt túi khí ghế trước khi có ghế trẻ em; nhắc quên trẻ trong xe | Có (hình dạng lưng ghế, tựa đầu) |
| 4 | infant_seat + facing | rear / front | Tắt túi khí khi nôi quay về sau ở ghế trước; nhắc quên em bé | Có (quai xách, vỏ nôi) |
| 5 | child (người là trẻ em) | có / không, theo ghế | Nhắc quên trẻ (child presence detection), quy định Euro NCAP | Có (S01, S03, S04, S05, S08 có trẻ nhưng v1.0 chưa cho gán) |
| 6 | object + type | bag / box / cup / other | Nhắc quên đồ khi rời xe; không nhầm vật với người khi đếm | Có (hình dạng), mất màu nên khó phân biệt túi/gối (S01, S07) |
| 7 | empty_seat | đếm theo ghế | Biết ghế trống để không kích hoạt nhắc dây an toàn, túi khí | Có |

## 2 câu hỏi leo thang

1. Câu hỏi: Ghế trẻ em hoặc nôi **đang có trẻ ngồi** thì gán thế nào? Guideline v1.0 nói không gán trẻ và `occupied` không có `yes`, nhưng file nhãn mới của coach lại thêm `occupied = yes`, còn `cabin_check` vẫn báo lỗi khi dùng `yes`.
   Khung ví dụ: G04 S01 (rear_right), S03 (rear_right), S04 (rear_left), S08 (rear_left); nôi có em bé ở S03, S05 (rear_left).
   Tạm gán thế nào và vì sao: vẽ box `child_seat` / `infant_seat`, không vẽ `person` cho trẻ, ghi `occupied = unknown` để đúng guideline v1.0 và qua `cabin_check`. Đề xuất v1.x: cho phép `occupied = yes` và thêm lớp `child` để phục vụ chức năng nhắc quên trẻ.

2. Câu hỏi: Nôi em bé đặt **nghiêng ngang ghế** (không quay hẳn về trước hay sau) thì `facing` ghi gì? Thuộc tính hiện chỉ có `rear` / `front`, không có `unknown` hay `sideways`.
   Khung ví dụ: G04 S03 và S05, nôi ở rear_left.
   Tạm gán thế nào và vì sao: ghi `front` vì từ camera nhìn thấy phía trong nôi; đề xuất thêm giá trị `unknown` cho `facing` để không phải đoán, đúng quy tắc chung 4.4-1.

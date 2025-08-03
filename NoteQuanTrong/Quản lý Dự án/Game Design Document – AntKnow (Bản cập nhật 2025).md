

# Game Design Document – AntKnow (Bản cập nhật 2025)

Game AntKnow mở rộng lối chơi cờ tỷ phú quen thuộc bằng cách kết **thẻ bài kỹ năng** và **hỏi-đáp kiến thức** để tạo ra trải nghiệm vừa giải trí vừa giáo dục[^1]. Bản GDD cập nhật này bổ sung hai cấu trúc bàn cờ mới, giải thích thuật ngữ then chốt, thêm sơ đồ flowchart, timeline trực quan và một bản tải về giàu định dạng để tiện tham khảo. Bạn có thể tải bản tóm tắt nhanh ở dạng Markdown tại đường dẫn.

## 1. Tổng quan thiết kế

### 1.1 Thông tin cơ bản

- **Tên game**: AntKnow[^1]
- **Thể loại**: Board Game -  Strategy -  Trivia -  Multiplayer[^1]
- **Nền tảng**: PC, Android, iOS (đa thiết bị, đa phòng)[^1]
- **Góc nhìn \& đồ họa**: Isometric 2.5D, phong cách Semi-Realistic tươi sáng dễ nhìn[^1]
- **Thông điệp**: “Chơi vui – Học hay” nhờ kho câu hỏi cộng đồng liên tục mở rộng[^1]


### 1.2 Điểm độc đáo

- Cơ chế **Monopoly + Quiz + Skill Cards** hiếm gặp trong thị trường VN[^1]
- **Rung Chuông Vàng**: 100 người chơi đấu loại trực tiếp kiến thức[^1]
- Cho phép PC và Mobile cùng phòng, giảm rào cản thiết bị[^1]
- Hệ thống **thẻ bài tiến hóa** tạo chiều sâu lâu dài nhưng không “pay-to-win” nhờ giới hạn số thẻ mang trận[^1]
- Kho câu hỏi mở, người chơi có thể đóng góp qua form duyệt nội dung[^1]


### 1.3 Thuật ngữ trọng yếu

| Thuật ngữ | Diễn giải |
| :-- | :-- |
| **Rung Chuông Vàng** | Chế độ *battle-royale* hỏi-đáp: tối đa 100 người, trả lời sai bị loại, người cuối cùng chiến thắng[^1] |
| **Thẻ bài kỹ năng** | Lá bài gắn một trong 5 chỉ số cơ bản; gồm **Thẻ Nội Tại** (buff vĩnh viễn) và **Thẻ Kích Hoạt** (dùng trong trận, có hồi chiêu)[^1] |
| **Tiến hóa** | Dùng thẻ/phụ kiện làm nguyên liệu để giảm hồi chiêu (thẻ) hoặc tăng độ bền (phụ kiện), tối đa 5★, mở khoá mỗi 10 cấp[^1] |

## 2. Cơ chế gameplay cốt lõi

Người chơi lần lượt tung hai xúc xắc (2–12) và di chuyển trên bàn cờ hình **Vuông** hoặc **Hai Vuông Gấp Khúc**[^1]. Sau khi dừng, trò chơi xử lý ô đến:

- **Ô nhà trống**: mua hoặc bỏ qua; nhà có 4 cấp + biệt thự[^1]
- **Ô nhà có chủ**: trả thuê hoặc mua lại với giá đề xuất[^1]
- **Ô Sự kiện**: rút thẻ event tích cực/tiêu cực (đi lùi, thưởng Gold, v.v.)[^1]
- **Ô Tai nạn**: dừng 3 lượt, thoát khi đổ đôi[^1]
- **Ô Tra khảo**: trả lời câu hỏi; sai nhận phạt ngẫu nhiên (mất nhà, tiền, dịch chuyển)[^1]
- **Ô Du lịch**: chọn dịch chuyển tới bất kỳ ô, trả phí[^1]
- **Ô Bắt đầu**: lãnh lương + tùy chọn nâng cấp nhà[^1]

Sau mỗi 5–8 lượt toàn bàn sẽ diễn ra **Tra Khảo Thường Niên** để giữ nhịp kiến thức[^1]. Người chơi có thể kích hoạt **Thẻ bài Kỹ năng** bất kỳ lúc nào đáp ứng điều kiện và hồi chiêu[^1].

### 2.1 5 chỉ số nhân vật

| Chỉ số | Tác dụng |
| :-- | :-- |
| **Luck** | +% xúc xắc “tốt” (ra đôi hoặc rơi vào ô trống) mỗi 200 điểm[^1] |
| **Resistance** | –% tiền thiệt hại/thuê; 100 điểm = –1%[^1] |
| **Intelligence** | +% thu nhập thuê nhà; 300 điểm = +1%[^1] |
| **Health** | +% lương khi qua Start; 300 điểm = +1%[^1] |
| **Agility** | +% cơ hội x2 tiền thuê; 500 điểm = +5%[^1] |

### 2.2 Thẻ bài kỹ năng tiêu biểu

| Tên | Loại | Hiệu ứng | Điều kiện | Hồi chiêu |
| :-- | :-- | :-- | :-- | :-- |
| **Chăm Chỉ** | Nội tại | +Health; luôn +10% lương khi qua Start[^1] | Trận bắt đầu | – |
| **Phá Hủy** | Kích hoạt | Phá 1 nhà trong phạm vi ±3 ô[^1] | Từ lượt 5 | 8 lượt |
| **Tráo Đổi** | Kích hoạt | Đổi nhà mình với người khác[^1] | Từ lượt 5 | 8 lượt |

## 3. Bản đồ \& bàn cờ

Game hiện có hai thiết lập bàn cờ, mỗi bản đồ dùng gạch màu để minh hoạ ô đặc biệt[^1].

### 3.1 Map 1 – Hình Vuông (World-City Theme)[^1]

### 3.2 Map 2 – Hai Vuông Gấp Khúc (Vietnam Theme)[^1]

Các ô đặc biệt luôn hiển thị chú thích màu (Tra khảo – tím, Tai nạn – đỏ, Bắt đầu – xanh lá, Event – cam, Du lịch – xanh dương)[^1].

## 4. Hệ thống nâng cấp \& tiến hóa

- **Nâng cấp**: dùng **EXP Card + AntCoin**; tối đa 50 cấp[^1].
- **Tiến hóa** (mỗi 10 cấp): tiêu hao thẻ/phụ kiện nguyên liệu để:
    - Giảm lượt hồi chiêu (đối với thẻ kỹ năng)[^1]
    - Tăng độ bền (đối với phụ kiện)[^1]
- **Độ bền phụ kiện** giảm sau trận; dùng **Búa Thường** (+10) hoặc **Búa Siêu Cấp** (+30) để sửa[^1].


## 5. Kinh tế \& tiền tệ

| Tiền tệ | Nguồn | Chi tiêu |
| :-- | :-- | :-- |
| **AntCoin (Gold)** | Thắng trận, nhiệm vụ ngày | Nâng cấp thẻ/phụ kiện[^1] |
| **DCoin (Diamond)** | Gói IAP | Mua rương hiếm, skin, battle-pass[^1] |
| **Tiền mặt** | Phát sinh trong trận | Mua nhà, trả thuê[^1] |
| **Tài sản** | Tiền mặt + Giá trị nhà | Quyết định phá sản/thắng[^1] |

> Quảng cáo dạng *reward-ads* và gói **Premium Subscription** (69 k–1,4 tr VND) mang doanh thu dài hạn mà không ảnh hưởng cân bằng[^1].

## 6. Chế độ Rung Chuông Vàng

- **Số người chơi**: tối đa 100[^1]
- **Luật**: mỗi vòng đặt câu hỏi trắc nghiệm 10–15 giây; trả lời sai bị loại ngay[^1]
- **Tăng khó**: về cuối độ khó cao dần; tốc độ câu hỏi nhanh hơn[^1]
- **Phần thưởng**: Top 1 nhận điểm kinh nghiệm lớn, khung danh hiệu đặc biệt[^1]


## 7. Hệ thống sự kiện \& cộng đồng

- **Ô Sự kiện**: 25+ lá bài ngẫu nhiên, ví dụ *Đi Lùi*, *Thừa Kế Gia Sản*, *Khế Ước Quỷ Dữ*[^1]
- **Đóng góp câu hỏi**: form online, đội QC duyệt hàng tuần để thêm database tránh lặp[^1]
- **Leaderboard**: xếp hạng mùa giải Elo-like, reset 3 tháng/lần[^1]


## 8. Lộ trình phát triển

Biểu đồ Gantt dưới đây minh hoạ 10 sprint từ 3/2025 đến 1/2026, chia 4 giai đoạn: Design (xanh lá), Development (xanh dương), Testing (vàng) và Launch (đỏ)[^1].

![Timeline phát triển game AntKnow (10 Sprint từ 3/2025 đến 1/2026)](https://ppl-ai-code-interpreter-files.s3.amazonaws.com/web/direct-files/59df8d548855ebd547454f860b6f3f38/6a011959-a73b-49a2-8e9f-d389f1f1aa73/23ff4292.png)

Timeline phát triển game AntKnow (10 Sprint từ 3/2025 đến 1/2026)

## 9. Sơ đồ luồng gameplay

Sơ đồ flowchart tóm lược toàn bộ vòng lặp lượt chơi – từ tung xúc xắc tới kiểm tra điều kiện thắng[^1].

![Flowchart Gameplay chính của game AntKnow](https://ppl-ai-code-interpreter-files.s3.amazonaws.com/web/direct-files/59df8d548855ebd547454f860b6f3f38/d9886807-e982-4b4f-a993-6cfbdac8e02e/33ad662d.png)

Flowchart Gameplay chính của game AntKnow

## 10. Kết luận

Phiên bản GDD mới chuẩn hoá thuật ngữ, đánh dấu rõ hai bản đồ, trực quan hoá quy trình gameplay và công bố timeline chi tiết để đội phát triển bám sát mốc hoàn thiện[^1]. Với cơ chế **Monopoly-Quiz-Card** cùng lộ trình công nghệ Unity + Netcode, AntKnow hứa hẹn trở thành lựa chọn “vừa học vừa chơi” hấp dẫn trên cả PC lẫn di động trong năm 2026[^1].

<div style="text-align: center">⁂</div>

[^1]: GameDesignDocument.pdf

[^2]: map1.jpg

[^3]: map2.jpg

[^4]: https://ppl-ai-code-interpreter-files.s3.amazonaws.com/web/direct-files/59df8d548855ebd547454f860b6f3f38/f922a129-2d92-4cc8-a21b-349f7d27295c/e870bf88.md


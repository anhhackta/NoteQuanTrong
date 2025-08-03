**Tài liệu Thiết kế Game (Game Design Document – GDD)**

# CardSpy

---

## 1. Tổng Quan Game

- **Tên Game:** CardSpy
- **Thể loại:** Hành động 3D đa người, kết hợp yếu tố chiến thuật tâm lý (Battle Royale + Social Deduction)
- **Nền tảng:** PC, Console
- **Engine:** Unity 3D (URP hoặc HDRP)
- **Mạng:** Photon Fusion hoặc Unity Netcode for GameObjects
- **Số người chơi/trận:** 4–8 người
- **Thời lượng trận đấu:** Khoảng 10–15 phút (có thể tuỳ chỉnh)
- **Điểm nhấn chính:**
  1. **Chiến thuật & Tâm lý** – Cơ chế lá bài bí ẩn, hoán đổi bài định kỳ.
  2. **Đồng minh & Phản bội** – Lập đội tạm thời, tính điểm bài chung.
  3. **Đa dạng vũ khí & item** – Các item lạ với cơ chế vật lý thú vị.
  4. **Tương tác xã hội mạnh** – Voice chat trực tiếp, mini-game nhiệm vụ kiếm SGold.
  5. **Trải nghiệm mới lạ** – Sự kết hợp giữa battle royale và bluffing như Among Us/Goose Goose Duck.

---

## 2. Vòng đời trận đấu (Game Loop)

1. **Lobby & Tùy chỉnh phòng:**
   - Người chơi tạo hoặc tham gia phòng, chọn thời gian đổi bài (mặc định 2 phút).
   - Tùy chỉnh nhân vật qua Ready Player Me.
2. **Bắt đầu trận đấu:**
   - Mỗi người nhận:
     - Một lá bài bí mật (2–10, J, Q, K, A, Joker, King).
     - Thanh HP 100/100.
     - 3 ô chứa item trống.
3. **Khám phá & Chiến đấu:**
   - Thu thập vũ khí, item và **SGold** từ rương hoặc nhiệm vụ mini-game.
   - Dùng SGold để mua vũ khí và vật phẩm tại các máy bán hàng.
4. **Cơ chế Ngất & Xét Bài:**
   - Khi HP về 0, người chơi **ngất** trong 10 giây.
   - Trong 10s này, nếu đối thủ xét bài và bài bạn thua, bạn bị loại (Specter).
   - Nếu không bị xét bài trong 10s, bạn hồi 20 HP và tiếp tục.
5. **Swap Phase – Đổi Bài:**
   - Cứ mỗi 2 phút (hoặc tùy chỉnh), diễn ra một trong 3 sự kiện ngẫu nhiên:
     1. **Normal Swap:** Đổi bài mới (2–A).
     2. **Joker Swap:** Mọi người nhận Joker (ẩn giá trị).
     3. **King Swap:** Chọn một người làm King (bài cao nhất) – King sẽ bị lộ trên map.
6. **Cơ chế Lập Đôi (Team-Up):**
   - Lập đội với 1 người khác:
     - Khi xét bài, nếu cả hai sống thì cộng điểm 2 lá bài.
     - Nếu một trong hai bị ngất, chỉ lá bài người còn lại được xét.
     - Nếu đội bị người khác xét bài và thua, cả 2 chết.
     - Nếu thành viên đi xét bài và thua, chỉ thành viên đó chết.
     - Vị trí đội hiển thị trên bản đồ.
7. **Spectator Mode:**
   - Người bị loại có thể xem trận đấu và chat với Specter khác.
8. **Chiến thắng:**
   - Người hoặc đội cuối cùng còn sống thắng trận.

---

## 3. Cơ chế Chi Tiết

### 3.1 Hệ thống Lá Bài

| Loại Bài       | Giá trị  | Hiệu ứng                                                                  |
| -------------- | -------- | ------------------------------------------------------------------------- |
| 2–10           | 2–10     | **+Tốc độ di chuyển** (thẻ cao = tốc độ cao hơn). Chỉ hiệu lực khi Combo. |
| J, Q, K        | 10       | **Face Card**, tăng sát thương nhẹ tùy J < Q < K khi Combo đội.           |
| A              | 1        | **+25 HP tối đa**, **+20% tốc độ di chuyển** (Combo đội).                 |
| Joker          | 10 (ẩn)  | **+ máu và sát thương nhiều**, ẩn đến khi xét bài. (Combo đội             |
| King (Sự kiện) | cao nhất | King bị lộ trên bản đồ, nắm bài cao nhất.                                 |
| Shield Card    | –        | bảo vệ khỏi xét bài 1 lần  (tiêu hao sau khi dùng) hồi 20 máu ngay.       |

**Combo Đội:** Nếu cả 2 thành viên có cùng lá bài, sẽ hiển thị bài của nhau và tăng sát thương (J/Q/K) hoặc cộng thêm điểm bài.

### 3.2 Vũ khí & Item

**Vũ khí:**

- **Đá (Rock):** Sát thương cao, ném chậm, đường đạn rơi mạnh.
- **Ná (Slingshot):** Bắn nhanh, sát thương thấp, đạn ít.
- **Dép (Flip-Flop):** Sát thương cao, tốc độ nhanh, độ lệch lớn, chỉ có 2 chiếc.
- **Lựu Đạn:** Gây sát thương diện rộng.

**Item hỗ trợ:**

- **Bẫy (Trap):** Giữ chân mục tiêu 3s.
- **Bom Khói:** Che tầm nhìn một khu vực nhỏ.
- **Radar:** Hiển thị kẻ địch trong bán kính 5s.
- **Shield Card Pickup:** Cộng thêm HP ảo (tối đa 50HP).
- **Bandit:** Hồi 15 HP.
- **First Aid Kit:** Hồi đầy HP.

### 3.3 Di chuyển

- Hệ thống chạy, nhảy, bò, ngồi.

### 3.4 Nhiệm vụ & SGold

- **Nhiệm vụ nhỏ:** Mini-game đơn giản (ví dụ hack panel, giải đố nhanh) như bên Among Us hay Goose Goose Duck.
- **Rương:** Sinh ngẫu nhiên trên map, chứa SGold ,item hoặc vũ khí.
- **SGold:** Dùng để mua vũ khí/item tại quầy bán hàng rải rác trên map.

### 3.5 Cơ chế Swap Phase

- Gồm Normal Swap, Joker Swap, King Swap.
- UI hiển thị đồng hồ đếm ngược, hiệu ứng lật bài khi đổi.

---

## 4. Thiết kế Map & Môi trường

- **Kích thước:** Arena 200×200m.
- **Địa hình:** Nhà cửa, vật cản, đường phố, chỗ ẩn nấp.
- **Máy bán hàng:** Vị trí chiến lược.
- **Thời tiết:** Ngẫu nhiên (mưa, sương mù, trời quang).
- **Safe Zone:** Tuỳ chọn co dần theo thời gian.

---

## 5. UI/UX

- **HUD:**
  - HP + Shield.
  - 3 ô item.
  - Đồng hồ đổi bài.
  - Hiển thị lá bài bản thân và đồng đội (khi lập đội).
- **Minimap:** Hiển thị King, vị trí đội.
- **Màn hình xét bài:** Show bài và kết quả thắng/thua.

---

## 6. Kỹ thuật & Lộ trình

- **Giai đoạn phát triển:**
  1. **Prototype (2–3 tuần):** Di chuyển, combat, xét bài cơ bản.
  2. **Alpha (4–6 tuần):** Cơ chế Swap, hệ thống ngất, SGold.
  3. **Beta (4–6 tuần):** Multiplayer đầy đủ, UI hoàn chỉnh, mini-game.
  4. **Release (3–4 tuần):** Tối ưu, bug fix, polish.

---

*GDD này đã hoàn thiện đầy đủ thông tin cho CardSpy, sẵn sàng xuất file PDF để trình bày.*


# Nam Chess (Cờ Nam) - Game Design Document

## Mục lục

- [1. Giới thiệu tổng quan](#1-giới-thiệu-tổng-quan)
- [2. Bàn cờ và thiết lập](#2-bàn-cờ-và-thiết-lập)
- [3. Quân cờ và cách di chuyển](#3-quân-cờ-và-cách-di-chuyển)
- [4. Luật chơi & Vòng lượt](#4-luật-chơi--vòng-lượt)
- [5. Điều kiện thắng/thua](#5-điều-kiện-thắngthua)
- [6. Triển khai bằng Unity](#6-triển-khai-bằng-unity)
- [7. UI/UX](#7-uiux)
- [8. Hệ thống xếp hạng và thành tựu](#8-hệ-thống-xếp-hạng-và-thành-tựu)
- [9. Kế hoạch phát triển](#9-kế-hoạch-phát-triển)
- [10. Thông điệp](#10-thông-điệp)

---

## 1. Giới thiệu tổng quan

### 1.1 Thông tin cơ bản

- **Tên game**: Nam Chess (Cờ Nam)
- **Thể loại**: Chiến thuật theo lượt (Turn-based Strategy)
- **Nền tảng phát triển**: Unity 2022.3 LTS
- **Nền tảng phát hành**: PC (Windows/Mac/Linux), Mobile (Android/iOS), Web (WebGL)
- **Số lượng người chơi**: 1–2 (Online hoặc Offline)
- **Độ tuổi khuyến nghị**: 8+
- **Thời gian chơi trung bình**: 15–30 phút

### 1.2 Ý tưởng cốt lõi

Nam Chess là trò chơi cờ chiến thuật độc đáo kết hợp yếu tố **may rủi từ xúc xắc**. Người chơi điều khiển 16 quân cờ trên bàn 9x9. Mỗi lượt tung xúc xắc quyết định **số bước di chuyển** và **loại quân nào được phép đi** (chỉ có Quan và Dân bị giới hạn theo giá trị xúc xắc, các quân khác chỉ cần thỏa điều kiện di chuyển trên bàn).

Game hỗ trợ:

- **Online Multiplayer** với xếp hạng ELO.
- **Offline** với AI thông minh (3 cấp độ khó).
- **Hot-seat mode** cho 2 người trên cùng thiết bị.

---

## 2. Bàn cờ và thiết lập

### 2.1 Bàn cờ

- **Kích thước**: 9x9 ô (81 ô).
- **Khu vực**:
  - **Sân nhà**: 4 hàng đầu (36 ô mỗi bên).
  - **Vùng trung lập**: Hàng giữa (9 ô).
  - **Vùng Vua**: 3x3 ô trung tâm sân nhà (Vua phải ở trong vùng này).

### 2.2 Ô đặc biệt

- **Ô Xanh (Green)** – 4 ô (2 mỗi bên sân).\
  *Hiệu ứng*: Quân đi vào ô xanh sẽ **lùi 1 ô** theo hướng vừa di chuyển.
- **Ô Đỏ (Red)** – 1 ô trung tâm.\
  *Hiệu ứng*: Quân đi vào ô đỏ sẽ **được di chuyển thêm 1 ô** theo bất kỳ hướng nào.

### 2.3 Sắp xếp quân cờ ban đầu

- **Mỗi bên có 16 quân**:
  - **Hàng 1 (hàng sau)**: 2 Bộ binh (B), 2 Tượng (A), 2 Quan (Q), 2 Cận vệ (T), 1 Vua (X).
  - **Hàng 2**: 2 Pháo (P) ở cột 2 và 8.
  - **Hàng 3**: 5 Dân (D) ở các cột lẻ (1, 3, 5, 7, 9).

---

## 3. Quân cờ và cách di chuyển

### 3.1 Cơ chế di chuyển cơ bản

- **Xúc xắc (1–6)** quyết định số ô phải di chuyển.
- **Quan (Q)** chỉ được phép di chuyển khi xúc xắc ra **4, 5, 6**.
- **Dân (D)** chỉ được phép di chuyển khi xúc xắc ra **1, 2, 3**.
- **Các quân khác (B, A, T, P)** có thể di chuyển với bất kỳ kết quả xúc xắc nào, miễn là thỏa điều kiện di chuyển và không bị cản.
- **Nếu không có quân nào hợp lệ với kết quả xúc xắc**, người chơi **mất lượt**.

### 3.2 Quy tắc từng quân

- **Vua (X)** – Di chuyển 1 ô thẳng, ngang hoặc chéo, **chỉ trong vùng Vua (3x3)**.
- **Dân (D)** – Di chuyển thẳng/ngang trong sân nhà, đa hướng khi vào sân đối thủ.
- **Quan (Q)** – Di chuyển thẳng/ngang đúng số ô xúc xắc (chỉ 4-6).
- **Tượng (A)** – Đi chéo đúng số ô xúc xắc.
- **Bộ binh (B)** – Đi thẳng/ngang đúng số ô xúc xắc.
- **Cận vệ (T)** – Đi thẳng/ngang/chéo nhưng chỉ trong sân nhà.
- **Pháo (P)** – Đi thẳng/ngang, ăn quân bằng cách **nhảy qua 1 quân làm giá pháo**.

---

## 4. Luật chơi & Vòng lượt

### 4.1 Cấu trúc lượt chơi

1. **Tung xúc xắc (1–6).**
2. **Xác định quân hợp lệ** dựa trên kết quả xúc xắc.
3. **Highlight các quân hợp lệ**.
4. **Người chơi chọn quân → hiển thị ô hợp lệ**.
5. **Chọn ô đích (đúng số ô bằng giá trị xúc xắc).**
6. **Di chuyển quân & áp dụng hiệu ứng ô đặc biệt.**
7. **Chuyển lượt cho đối thủ.**

### 4.2 Quy tắc di chuyển & ăn quân

- Không đi qua quân cùng phe.
- Tất cả quân (trừ Pháo) ăn quân đối thủ khi dừng tại ô chứa quân đó.
- Pháo ăn quân bằng cơ chế nhảy qua 1 quân làm giá pháo.
- Nếu không có quân hợp lệ, bỏ lượt.
- Nếu không còn nước đi, thua ngay.

---

## 5. Điều kiện thắng/thua

- **Thắng**: Ăn được Vua đối thủ hoặc khiến đối thủ không còn nước đi.
- **Hòa**: Hai bên đồng ý, hoặc lặp lại thế 3 lần, hoặc 50 lượt không ăn quân.

---

## 6. Triển khai bằng Unity

### 6.1 Kiến trúc chính

```csharp
public class BoardManager : MonoBehaviour {
    public GameObject[,] board = new GameObject[9,9];
    public List<Piece> whitePieces, blackPieces;
    public GameState currentState;
}

public class DiceSystem : MonoBehaviour {
    public int RollDice() => Random.Range(1, 7);
}
```

### 6.2 Multiplayer

- **Online**: Unity Netcode + Relay + Lobby + ELO Ranking.
- **Offline**: AI với Minimax + Alpha-Beta Pruning.

### 6.3 Tối ưu đa nền tảng

- **PC**: 60-120 FPS.
- **Mobile**: Android 7.0+, iOS 12+.
- **Web**: WebGL.

---

## 7. UI/UX

- **Menu chính**: Online, Offline, Local, Hướng dẫn, Cài đặt, Leaderboard.
- **HUD**: Lượt hiện tại, xúc xắc, timer, chat (online).
- **Hiệu ứng**: Highlight quân, hiệu ứng ô đặc biệt, animation khi ăn quân.

---

## 8. Hệ thống xếp hạng và thành tựu

- **ELO**: 1000 → 3000 (Bronze → Master).
- **Thành tựu**: Chuỗi thắng, ăn quân đặc biệt, không mất quân.
- **Nhiệm vụ tuần**: Thử thách AI hoặc thắng bằng quân nhất định.

---

## 9. Kế hoạch phát triển

- **Tháng 1–3**: Luật chơi, UI cơ bản.
- **Tháng 4–5**: AI, âm thanh, hiệu ứng.
- **Tháng 6–7**: Online Multiplayer.
- **Tháng 8–9**: Beta test, phát hành.

---

## 10. Thông điệp

**"Nam Chess – Sự kết hợp chiến thuật và may mắn, chơi mọi lúc, mọi nơi."**


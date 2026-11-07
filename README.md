# 🎣 Hồ Câu Cá Giải Trí Online — TikTok Live RPC (9:16 Interactive Fishing Stream)

Hệ thống phát trực tiếp tương tác (**Interactive TikTok Live Stream & JSON-RPC 2.0**) chuẩn khung dọc **9:16 (`1080×1920`)** dành cho **OBS Studio / TikTok Live Studio**, chạy siêu nhẹ trên **Bun.js** và tích hợp giọng đọc AI tiếng Việt **ZeroTTS (`zeroweight-ai/ZeroTTS`)**.

Người xem trên TikTok Live tương tác trực tiếp qua **Thả tim (Like)**, **Bình luận (Comment)**, **Chia sẻ / Follow** và **Tặng quà (Gift)** để buông cần câu cá trên màn hình Hồ Nước Sơn Thủy Hữu Tình:
- 🪱 **Thả Thính Dụ Cá (Like / Thả tim)**: Ném thính thơm tõm xuống nước, sủi bọt tăm và thu hút đàn cá tụ lại quanh phao câu.
- 🎣 **Quăng Cần & Thả Phao (Bình luận `quăng cần`, `câu cá`, `thả câu`)**: Cần thủ vung cần vút gió ra giữa hồ, phao câu nhấp nhô theo làn sóng nước.
- 🐟 **Giật Cần Bắt Cá (Bình luận `giật cần`, `lên cá`, `cá to`, `bắt cá`)**: Phao câu chìm giật rung bần bật, kéo vút cá lên khỏi mặt nước kèm hiển thị **Thẻ Chiến Tích Bắt Cá** (loài cá, cân nặng, độ hiếm) và giọng đọc AI thông báo chúc mừng!
- 📯 **Thổi Còi Báo Cá (Follow / Share hoặc bình luận `thổi còi`)**: Tiếng còi bến tàu vang rền, đàn cá nhảy vọt lên khỏi mặt nước.
- 🦐 **Mồi Thượng Hạng (Tặng quà 5–99 xu)**: Dùng mồi câu xịn bắt ngay các loài cá Cực Phẩm (Cá Koi Ngũ Sắc, Cá Trê Hoàng Kim, Cá Tầm Hoàng Gia...).
- 🐉 **Đại Chiến Thủy Quái (Tặng quà ≥ 100 xu)**: Kéo lên huyền thoại **Cá Rồng Kim Long Quá Bối** hoặc **Thủy Quái Hồ Sâu (Cá Hô 88kg)**, hiệu ứng bão bọt nước và bảng vinh danh toàn màn hình!
- 👑 **Bảng Vàng Cần Thủ (Vua Sát Cá & 6 Ghế Câu VIP)**: Tự động xếp hạng Top cần thủ có tổng cân nặng cá và chiến tích cao nhất trên 6 ghế câu ven hồ.

---

## ⚡ Kiến Trúc & Tối Ưu Hóa Hiệu Suất (Siêu Nhẹ CPU/GPU)

- **Runtime**: Chạy trực tiếp trên **Bun.js** (`~0.1% CPU` khi chờ).
- **Canvas Particle Engine (`public/js/particles.js`)**:
  - Khóa tốc độ vẽ ở **30 FPS** ổn định, tự động tạm dừng khi ẩn tab (`document.hidden`).
  - Pre-render toàn bộ Bong bóng nước, Gợn sóng elip 2.5D, Giọt nước bắn và Bóng cá ra Offscreen Canvas 1 lần duy nhất lúc khởi tạo.
- **ZeroTTS Worker (`tts_worker.py`)**:
  - Tiến trình Python thường trú nạp sẵn model `zeroweight-ai/ZeroTTS` giọng Mai Chi hào sảng.
  - Tổng hợp nguyên câu trong 1 lần gọi, chuẩn hóa âm lượng và fade mượt mà.
- **Bảo Vệ WebSocket & Chặn Crash**:
  - Bắt lỗi toàn cục `process.on('uncaughtException')` và bảo vệ WebSocket client không bị sập khi TikTok Live ngắt kết nối.

---

## 🚀 Hướng Dẫn Cài Đặt & Chạy Nhanh

### 1. Yêu cầu hệ thống
- [Bun.js](https://bun.sh/) (`>= 1.1`)
- Python `3.10+` & [`uv`](https://github.com/astral-sh/uv)

### 2. Cài đặt thư viện
```bash
# Cài đặt dependencies cho Bun / Node
bun install

# Cài đặt ZeroTTS vào môi trường ảo
uv pip install --python .venv/bin/python zerotts pillow
```

### 3. Khởi chạy Server
```bash
bun start
# Hoặc chế độ tự động reload khi sửa code:
bun run dev
```

Mặc định server chạy tại cổng `3000`:
- **Màn hình Live 9:16 + Điều khiển nhanh**: [http://localhost:3000](http://localhost:3000)
- **Màn hình OBS Browser Source (Sạch 9:16)**: [http://localhost:3000/?obs=1](http://localhost:3000/?obs=1) *(Đặt kích thước Browser Source trong OBS là `1080 × 1920`)*
- **Bảng điều khiển Admin & RPC**: [http://localhost:3000/admin](http://localhost:3000/admin)

---

## 🎮 Bảng Quy Tắc Tương Tác TikTok Live & 9 Quà Tặng Chuẩn

### 1. Tương tác Thường & Bình luận
| Sự kiện TikTok Live | Từ khóa / Điều kiện | Hành động trên Hồ Câu | Điểm Cần Thủ |
| :--- | :--- | :--- | :---: |
| **Thả tim (Like)** | Mỗi đợt thả tim | Ném mồi thính sủi bọt nước dụ đàn cá tụ lại + Tích điểm Bão Cá | `+1` / tim |
| **Follow / Share** | Theo dõi hoặc chia sẻ | Thổi còi bến tàu ngân vang + Cá nhảy tung tăng | `+15` |
| **Bình luận Thả Thính** | `thả thính`, `mồi`, `thính` | Ném 5 nắm thính thơm xuống nước | `+5` |
| **Bình luận Quăng Cần** | `quăng cần`, `câu cá`, `thả câu` | Vung cần xé gió, phao câu rơi xuống hồ | `+5` |
| **Bình luận Giật Cần** | `giật cần`, `lên cá`, `cá to`, `bắt cá` | Giật cần, kéo lên chú cá ngẫu nhiên + Mở thẻ cá kèm **Avatar** + Đọc TTS | Theo độ hiếm cá |
| **Bình luận Thủy Quái** | `thủy quái`, `cá rồng`, `kim long` | Thử vận may săn cá quý hiếm hoặc cực phẩm | Theo loài cá |

### 2. Danh mục 9 Quà Tặng TikTok Live Chuẩn
| Quà tặng | Giá trị | Icon | Hiệu ứng trên Hồ Câu | Phần thưởng cá |
| :--- | :---: | :---: | :--- | :--- |
| **🌹 Hoa hồng** | `1 xu` | 🌹 | Mưa cánh hoa hồng rực rỡ mặt hồ | Bắt Cá Quý Hiếm (Chép Vàng, Cá Diếc) |
| **🐱 Đỉnh** | `1 xu` | 🐱👍 | Mèo Thần Tài giơ ngón cái cổ vũ | Bắt Cá Tươi Ngon may mắn |
| **🎮 GG** | `1 xu` | 🎮 | Chữ GG 3D phát sáng, khích lệ bến câu | Bắt Cá Quý Hiếm |
| **🕹️ Tay cầm chơi game** | `100 xu` | 🕹️ | **ĐẠI CHIẾN THỦY QUÁI**: Sấm chớp, bọt nước tung trời, Banner rồng vàng vinh danh Avatar | **Cá Rồng Kim Long Quá Bối / Cá Hô 88kg** |
| **🥰 Yêu bạn** | `1 xu` | 🥰 | Đàn cá xếp hình trái tim, lan tỏa yêu thương | Bắt Cá Quý Hiếm |
| **🐷 Chú heo may mắn** | `10 xu` | 🐷🎃 | Heo vàng đội bí ngô mang tài lộc đại cát | **Cá Cực Phẩm (Cá Koi, Cá Tầm Hoàng Gia)** |
| **🎵 TikTok** | `1 xu` | 🎵 | Logo TikTok 3D xoay vòng, sóng nhạc rộn rã | Bắt Cá Quý Hiếm |
| **🫰 Bắn tim** | `5 xu` | 🫰❤️ | Cơn mưa tim bay phấp phới, mồi hảo hạng | **Cá Quý Hiếm / Cực Phẩm (Cá Trắm Đen Khủng)** |
| **😉 Hiểu ý tôi chứ** | `1 xu` | 😉💖 | Biểu cảm nháy mắt siêu đáng yêu | Bắt Cá May Mắn |

---

## ⏱️ Cơ Chế Câu Cá: Miễn Phí (1 Phút) vs Donate (Lập Tức)

1. **Người xem miễn phí (Bình luận / Quăng cần / Không gửi quà)**:
   - **Thời gian chờ mặc định: 1 phút (60 giây)**.
   - Khi người xem bình luận bất kỳ (`câu cá`, `quăng cần`, chào hỏi hoặc gửi lời chúc): Hệ thống tự động xếp họ vào 1 ghế quanh bờ hồ, vung cần buông dây cước xuống nước và phao câu nhấp nhô.
   - Nhân vật cần thủ sẽ kiên nhẫn thả câu trong 60 giây, trên đầu xuất hiện bong bóng đếm ngược thời gian thực (`⏱️ Đang đợi cá... Xs`).
   - Nếu bình luận tiếp trong khi đang chờ, hệ thống thông báo thời gian còn lại mà không ngắt phiên câu.
   - **Sau đúng 1 phút (60 giây)**: Cá cắn câu tự động! Cần thủ giật cần, phao kéo chìm, giật lên một chú **cá ngẫu nhiên** (random fish) từ hồ câu!

2. **Người xem DONATE (Tặng quà xu TikTok Live)**:
   - **LẬP TỨC câu được cá random ngay và luôn**, không cần chờ 1 phút!
   - Hủy bỏ bộ đếm 1 phút nếu cần thủ đó đang trong phiên câu miễn phí.
   - Độ hiếm cá theo giá trị quà tặng:
     - `1 xu` (Hoa hồng, Đỉnh, GG, Yêu bạn, TikTok, Hiểu ý): Bắt cá random Phổ Thông hoặc Quý Hiếm.
     - `5–10 xu` (Bắn tim, Chú heo may mắn): Bắt cá random Quý Hiếm hoặc Cực Phẩm.
     - `≥ 100 xu` (Tay cầm chơi game): Bắt ngay huyền thoại **Cá Rồng Kim Long Quá Bối** hoặc **Thủy Quái Hồ Sâu (88kg)**!
   - Kích hoạt âm thanh Fanfare hoành tráng, hiệu ứng pháo nước và mở Bảng Chiến Tích vinh danh Avatar người tặng.

---

## 🌊 Tính Năng Đa Cần Thủ Vòng Quanh Bờ Hồ (Shore Anglers Ring)
1. **18 Vị Trí Cần Thủ Ngồi Quanh Hồ**:
   - Thay thế toàn bộ hình tượng 1 cần thủ đơn độc trước đây. Mỗi người xem là một cần thủ riêng biệt có ghế xếp dã ngoại, nón lá Việt Nam, áo gile, cần câu carbon, dây cước SVG và giỏ cá bên cạnh.
   - Ghế phân bố theo 4 bờ: Bờ Xa Phía Bắc (5 ghế), Bờ Cỏ Phía Tây (4 ghế), Bến Gỗ Phía Đông (4 ghế), Bờ Tiền Cảnh Phía Nam (5 ghế VIP).
2. **Hiển Thị Avatar Người Dùng Ở Mọi Nơi**:
   - **Khuôn mặt Cần thủ trên bờ hồ**: Avatar tròn sắc nét có viền phát sáng theo thứ hạng (`🥇 TOP 1` đội vương miện vàng).
   - **Thẻ Chiến Tích Bắt Cá (`#catchModal`)**: Avatar tròn viền vàng rực rỡ của cần thủ vừa giật cá.
   - **Popup Donate Nổi Bật (`#giftAlertToast`)**: Banner sang trọng hiển thị avatar người tặng, vương miện, tên quà và số xu.
   - **Banner Đại Chiến Thủy Quái (`#leviathanBanner`)**: Avatar người tặng quà 100 xu đặt trang trọng giữa vầng hào quang rồng vàng.
   - **Dòng Chat Nổi Màn Hình (`#liveChatOverlay`)**: Mọi comment và tương tác trôi mượt mà với avatar tròn 30px.
   - **Thanh HUD Đáy (`#hudActiveNotice`)**: Cập nhật avatar thật và trạng thái câu cá thời gian thực.
3. **Mục Tiêu Cộng Đồng & Giờ Vàng Bão Cá (Community Frenzy Bar)**:
   - Thanh tiến trình 500 điểm tích lũy chung từ mọi lượt Thả tim, Bình luận và Tặng quà.
   - Khi đạt 100%: Kích hoạt **Giờ Vàng Bão Cá 60 giây (X2 Điểm & Cân Nặng)** cho tất cả khán giả!

---

## 🔌 Giao Thức JSON-RPC 2.0 (`POST /rpc` & `ws://localhost:3000/ws`)

### 1. Giật cần bắt cá
```bash
curl -X POST http://localhost:3000/rpc \
  -H "Content-Type: application/json" \
  -d '{
    "jsonrpc": "2.0",
    "id": 1,
    "method": "fishing.hookFish",
    "params": {
      "user": "Hải Đăng Cần Thủ",
      "wish": "Săn cá chép giòn 5 ký!"
    }
  }'
```

### 2. Thả thính dụ cá
```bash
curl -X POST http://localhost:3000/rpc \
  -H "Content-Type: application/json" \
  -d '{
    "jsonrpc": "2.0",
    "id": 2,
    "method": "fishing.castBait",
    "params": {
      "user": "Tuấn Cần Thủ",
      "count": 5
    }
  }'
```

### 3. Săn Thủy Quái (Quà Lớn)
```bash
curl -X POST http://localhost:3000/rpc \
  -H "Content-Type: application/json" \
  -d '{
    "jsonrpc": "2.0",
    "id": 3,
    "method": "fishing.catchLeviathan",
    "params": {
      "user": "Đại Cần Thủ VIP",
      "coins": 199
    }
  }'
```

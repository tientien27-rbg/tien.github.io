# rkt.github.io

# Hướng Dẫn Bắt Đầu Sử Dụng Bot Tín Hiệu 🚀

## 📌 Mục Lục

* [1. Tính năng chính](#-tính-năng-chính)
* [2. Cài đặt & chạy](#-cài-đặt--chạy)
* [3. Lệnh cơ bản (slash commands)](#-lệnh-cơ-bản-slash-commands)
* [4. Menu & chỉ báo trong bot](#-menu--chỉ-báo-trong-bot)

  * [4.1. Spot](#41-spot)
  * [4.2. Volume/MarketCap (V/C)](#42-volumemarketcap-vc)
  * [4.3. Volume Delta (CVD ngắn hạn theo giao dịch)](#43-volume-delta-cvd-ngắn-hạn-theo-giao-dịch)
  * [4.4. Tỷ lệ Long/Short cao](#44-tỷ-lệ-longshort-cao)
  * [4.5. Futures: OI/Funding/Borrow](#45-futures-oifundingborrow)
  * [4.6. Smart Money](#46-smart-money)
* [5. Giải thích dữ liệu & cách đọc](#-giải-thích-dữ-liệu--cách-đọc)
* [6. Cảnh báo tự động (Job)](#-cảnh-báo-tự-động-job)
* [7. Lưu ý kỹ thuật & giới hạn API](#-lưu-ý-kỹ-thuật--giới-hạn-api)
* [8. FAQ](#-faq)

---

## ✅ Tính năng chính

* **Top Vol/Tăng/Giảm 24h** (Spot, cặp USDT).
* **V/C (Volume/MarketCap)**: xếp hạng theo tỉ lệ khối lượng giao dịch so với vốn hóa (24h & 30m).
* **Volume Delta**: chênh lệch buy/sell theo lệnh khớp (N trade, 1h, 24h).
* **Bộ quét Spot**:

  * Volume spike theo khung (5m/30m/4H/D1).
  * Trade-count spike (lọc lệnh lớn, trung bình size tối thiểu).
  * Big trade (giá trị khớp lớn nhất trong 4H hoặc 1D).
* **Futures**:

  * OI spike (tăng/giảm đột biến) theo 30m/4H/D1.
  * Funding list (24h, dương/âm).
  * “Borrow ratio” proxy bằng **Taker long/short Ratio 1D** (mạnh/yếu).
* **Smart Money**:

  * Xem **Top Trader** (Accounts/Positions) cho **coin đang chọn**.
  * **Taker Buy/Sell** cho coin đang chọn.
  * **Top list toàn thị trường** theo 6 nhóm: Acc Long/Short, Pos Long/Short, Taker Buy/Sell (5m/30m/4H/D1).
* **Cảnh báo tự động** (phút): tóm tắt tín hiệu Spot (volume spike, trade-count spike, big trade).

---

## ⌨️ Lệnh cơ bản (slash commands)

* `/start` – Mở menu chính.
* `/help` – Hướng dẫn sử dụng bot.
* `/ping` – Xem kết nối có bị lag không.
* `/coin` – Xem/đổi coin mặc định (ví dụ: `/coin btc`, `/coin solusdt`).
* `/gia` – Giá + %24h + so sánh Vol 24h với 24h trước.
* `/vc` – Tính V/C (Vol24h / MarketCap).
* `/volumedelta` – Δ 1h và 24h cho coin mặc định.
* `/oi` – Snapshot OI 24h (USDM & COINM).
* `/cvd` – CVD 24h vs 24–48h trước.
* `/funding` – Funding bình quân 24h vs 24–48h trước.
* `/long`, `/short` – Bot hỏi khung (5m/30m/4H/D1).

  * Alias nhanh: `/long5m`, `/long30m`, `/longh4`, `/longd1`, tương tự cho short.
* `/smart` – Mở nhanh menu **Smart Money**.
* `/alerts_on` – Bật cảnh báo tự động (mặc định 60s).
* `/alerts_off` – Tắt cảnh báo tự động (mặc định 60s).
* `/scan` – Tìm coin scan trong top mình cần tìm để lọc ra coin tìm năng, có volume mua thật không phải bot đẩy để marketing.
* `/scangem` – Tìm coin trong hết tất cả ở sàn cho ra kết quả delta/(v/mc) từ trên xuống dưới.
* `/scantim` – Tìm coin mình tìm xem volume đó thật hay là ảo.

---

## 🧭 Menu & chỉ báo trong bot

### 4.1. Spot

* **📈 Volume spike** – Tìm nến hiện tại có **khối lượng đột biến** nến trước.
* **🧨 Trade-count spike** – Tìm nến có **số lệnh** tăng đột biến.
* **💥 Big trade** – Giá trị giao dịch lớn nhất trong khung 4H hoặc 1D.

### 4.2. Volume/MarketCap (V/C)

* **⬆️ V/C cao 24h / 30p** – Vol lớn so với vốn hóa (vốn nhỏ nhưng giao dịch sôi động).
* **⬇️ V/C thấp 24h / 30p** – Lọc dự án vol thấp so với MC.


### 4.3. Volume Delta (CVD ngắn hạn theo giao dịch)

* **Δ dương/âm (N trade)** – Chênh lệch buy/sell.
* **Δ 1h / 24h** – Chênh lệch buy/sell.

### 4.4. Tỷ lệ Long/Short cao

* Toàn bộ người dùng futures.
* Top theo **% Long** hoặc **% Short** cho từng khung (5m/30m/4H/D1).

### 4.5. Futures: OI/Funding/Borrow

* **OI đột biến (⬆️/⬇️)**.
* **Funding (24h)** – Trung bình funding 24h (dương/âm).
* **Borrow Ratio (24h)** – Dùng **Taker long/short Ratio 1D** như proxy:

  * **Mạnh**: ratio > 1
  * **Yếu**: ratio < 1

### 4.6. Smart Money

Bộ 3 góc nhìn về **“tay to”**:

1. **Top Trader (coin đang chọn)**

   * **👤 Accounts**: % tài khoản top đang Long/Short.
   * **💼 Positions**: % **khối lượng vị thế** Long/Short của top.

2. **🛒 Taker Buy/Sell (coin đang chọn)**

   * Tỉ lệ lệnh **chủ động** mua/bán (order flow), kèm xu hướng kỳ trước.

3. **🏆 Top list toàn thị trường** (chọn nhóm → chọn khung 5m/30m/4H/D1)

   * **Acc Long / Acc Short**
   * **Pos Long / Pos Short**
   * **Taker Buy / Taker Sell**

> **Khác biệt với “Tỷ lệ Long/Short cao”**:
>
> * *Tỷ lệ Long/Short cao* = **toàn thị trường** (đám đông).
> * *Smart Money* = **nhóm top traders** + vị thế + dòng lệnh chủ động → thiên về “tay to”.

---

## 🧠 Giải thích dữ liệu & cách đọc

* **V/C** = `Volume giao dịch / MarketCap`
  Dự án vốn hoá nhỏ nhưng vol lớn → V/C cao, tiềm năng biến động mạnh.
* **Volume Delta / CVD**
  Dương → mua chủ động áp đảo; Âm → bán chủ động áp đảo. Dùng để xác nhận breakout hoặc phát hiện phân kỳ.
* **Global Long/Short Account Ratio**
  % tài khoản (tất cả user) đang Long/Short.
* **Top Trader Acc/Pos Ratio**
  * *Acc* = tỷ lệ tài khoản top.
  * *Pos* = tỷ trọng **khối lượng vị thế** của top.
* **Taker Buy/Sell Ratio**
  Đo **lệnh khớp chủ động** → phản ánh **dòng tiền** vào/ra nhanh.
* **Open Interest (OI)**
  ΔOI lớn bất thường (kèm điều kiện giá trị tuyệt đối) → có **mở/đóng** vị thế đáng kể.
* **Funding**
  Dương cao có thể báo **long crowded**; âm sâu báo **short crowded** (cần kết hợp giá/OI/flow).

---

## 🔔 Cảnh báo tự động (Job)

* Bật bằng `/alerts_on`, tắt `/alerts_off`.
* Gửi tóm tắt:

  * 📈 3 dòng đầu của **Volume spike 5m**
  * 🧨 3 dòng đầu của **Trade-count spike 5m**
  * 💥 3 dòng đầu của **Big trade 4H**

---

## ⚙️ Lưu ý kỹ thuật & giới hạn API

* Dùng session `requests` + `Retry` để ổn định gọi API.
* Lọc cặp Spot chỉ lấy **USDT** (bỏ **UP/DOWN/BULL/BEAR**).
* CoinGecko rate-limit: khi gọi nhiều trang MC có thể chậm; code đã **giới hạn trang** và dùng lại giữa các bước.
* Đối với **delta** qua `aggTrades`, code cắt theo `DELTA_TIME_CAP_TRADES` để tránh tải quá lớn.
* Một số endpoint futures đôi lúc time-out → bot đã bắt lỗi và trả về thông báo “không có dữ liệu”.

---

## ❓ FAQ

**Q1. Vì sao ấn “Top list Smart Money” rồi chọn nhóm mà không thấy dữ liệu?**
– Hãy thử lại khung lớn hơn vì khung nhỏ binance chưa trả dữ liệu. Thử khung **30m/4H/D1** hoặc thử lại sau một lát.

**Q2. “Tỷ lệ Long/Short cao” khác gì “Smart Money”?**
– *Tỷ lệ Long/Short cao* là **toàn bộ user**. *Smart Money* là **Top Traders** và có thêm **Pos** (khối lượng vị thế) + **Taker** (order flow).

**Q3. Big trade có phải tổng vol không?**
– Không. Đây là **giá trị giao dịch lớn nhất** tìm được trong cửa sổ thời gian (4H/D1).

**Q4. V/C cao có nghĩa nên mua?**
– Không. V/C chỉ là **điểm bất thường về dòng tiền** so với vốn hóa. Hãy kết hợp thêm OI/Funding/Price Action/Smart Money.

---

### 📬 Liên hệ

* Vấn đề/kho lỗi: mở **Issues** trên repo.
* Đóng góp/PR: chào mừng bạn thêm chỉ báo, tối ưu hiệu năng và UX.

---

> Chúc bạn giao dịch an toàn & kỷ luật. Dùng các chỉ báo như **dấu hiệu** – **không phải** khuyến nghị đầu tư.

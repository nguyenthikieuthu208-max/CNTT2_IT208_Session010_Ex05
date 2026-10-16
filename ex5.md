


PHẦN 1: PHÂN TÍCH HỆ THỐNG (INPUT - PROCESS - OUTPUT)

1. Mô hình dòng chảy dữ liệu IPO

-   **Input (Đầu vào):** Dữ liệu thô về nhiệt độ, độ ẩm đất đo từ cảm biến phần cứng và lệnh điều khiển từ xa của người dùng qua App di động.
-   **Process (Xử lý):** Vi xử lý trung tâm (SoC) phân tích dữ liệu, so sánh với các ngưỡng thiết lập và đưa ra quyết định logic kích hoạt thiết bị ngoại vi.
-   **Output (Đầu ra):** Kích hoạt rơ-le mở van nước, bật máy phun sương, còi cảnh báo và cập nhật dữ liệu trực quan lên màn hình giám sát.

2. Sơ đồ phối hợp phần cứng hệ thống

text

```
[Cảm biến Độ ẩm/Nhiệt độ] ──(Dữ liệu thô)──> [Bộ xử lý SoC Trung tâm] ──(Lệnh điều khiển)──> [Rơ-le/Máy bơm van điện]

```


----------

PHẦN 2: FILE HƯỚNG DẪN KỸ THUẬT CHUYÊN NGHIỆP (`README.md`)


markdown

```
# 🚀 Dự án Hệ thống Giám sát & Tưới tự động Smart-Farm

*Hệ thống tích hợp công nghệ IoT chuyên sâu giúp tự động hóa quy trình chăm sóc, tối ưu hóa lượng nước và nâng cao năng suất tối đa cho trang trại hoa Lan.*

---

## 1. Sơ đồ kiến trúc Hệ thống
Dưới đây là sơ đồ kết nối và vận hành cấu trúc mạng thiết bị trong trang trại:

![Sơ đồ kiến trúc kết nối phần cứng và luồng dữ liệu Smart Farm](https://unsplash.com)

---

## 2. Hướng dẫn cài đặt & Khởi chạy hệ thống
Kỹ sư và người vận hành truy cập vào Terminal máy chủ và thực thi chuỗi lệnh sau để thiết lập môi trường:

```bash
# Bước 1: Sao chép mã nguồn hệ thống về bộ xử lý trung tâm
git clone https://github.com

# Bước 2: Di chuyển vào thư mục dự án và cài đặt thư viện phần cứng
cd smart-farm
pip install -r requirements.txt

# Bước 3: Khởi chạy chương trình giám sát ngầm hệ thống
python main.py --mode=production
```

---

## 3. Tính năng cốt lõi & Danh sách nghiệm thu (Task List)
- [x] Tự động cập nhật chỉ số độ ẩm đất và nhiệt độ môi trường theo thời gian thực.
- [x] Kích hoạt hệ thống phun sương tự động khi nhiệt độ vượt ngưỡng an toàn.
- [ ] Tích hợp tính năng gửi tin nhắn cảnh báo khẩn cấp qua Telegram khi mất nước.
- [ ] Đồng bộ hóa lịch sử tưới tiêu lên điện toán đám mây theo định kỳ hàng tuần.

---

## 4. Bảng thông số kỹ thuật Thiết bị (Table)

| Thành phần thiết bị | Mã hiệu Phần cứng | Chức năng chính | Thông số vận hành |
| :--- | :---: | :--- | :---: |
| Bộ vi xử lý trung tâm | SoC ESP32-WROOM | Điều khiển, phân tích dữ liệu | Wi-Fi & Bluetooth, 5V DC |
| Cảm biến Độ ẩm đất | SHT31-D | Thu thập dữ liệu độ ẩm | Sai số \(\pm 2\%,\) chuẩn IP68 |
| Thiết bị đầu ra | Rơ-le cơ học 4 kênh | Đóng/Ngắt dòng điện máy bơm | Chịu tải tối đa 220V AC |

---

## 5. Cơ chế vận hành chuyên sâu của Hệ thống

### 5.1. Chu kỳ xử lý lệnh của CPU (Fetch - Decode - Execute)
Khi hệ thống nhận lệnh kích hoạt máy bơm tưới Lan, bộ vi xử lý (SoC) thực hiện chu kỳ nạp và xử lý lệnh liên tục tại các thanh ghi:
> **1. Fetch (Nhận lệnh):** Khối điều khiển CPU tiến hành trích xuất mã lệnh bật máy bơm từ bộ nhớ RAM hệ thống đưa vào thanh ghi chỉ thị.
> 
> **2. Decode (Giải mã):** Bộ giải mã lệnh dịch mã máy thô thành các tín hiệu điều khiển phần cứng tương ứng cho chân tín hiệu GPIO.
> 
> **3. Execute (Thực thi):** CPU gửi xung điện áp cao ra chân GPIO kết nối với Rơ-le, đóng mạch và kích hoạt máy bơm nước chạy vật lý ngoài đời thực.

### 5.2. Quy trình chuyển hóa dữ liệu theo mô hình DIKW (Kim tự tháp)
Hệ thống vận hành dựa trên sự nâng cấp giá trị thông tin theo 4 tầng cấp độ vững chắc:
1. **Data (Dữ liệu thô):** Cảm biến đọc và trả về một con số nguyên đơn thuần: `38`.
2. **Information (Thông tin):** Hệ thống gán ngữ cảnh cho con số: *"Độ ẩm đất của luống hoa Lan hiện tại đang ở mức cực thấp: 38%"*.
3. **Knowledge (Tri thức):** Đối chiếu với quy chuẩn nông nghiệp: *"Hoa Lan cần độ ẩm từ 60% trở lên để sinh trưởng tốt, mức 38% sẽ làm rễ cây bị khô héo"*.
4. **Wisdom (Trí tuệ/Hành động):** Đưa ra quyết định thông minh tối ưu: SoC tự động phát lệnh mở van điện tử tưới nước trong đúng 5 phút, giải cứu luống hoa kịp thời mà không cần con người can thiệp.

```


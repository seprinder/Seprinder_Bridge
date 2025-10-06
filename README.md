# Seprinder_Bridge — Hướng dẫn kết nối máy in và website

Công cụ giúp **kết nối website [Seprinder.com](https://seprinder.com)** với **máy in 3D chạy Klipper**

---

## Chuẩn bị

* Máy in 3D đang chạy **Klipper** (trên Raspberry Pi hoặc SBC chạy Linux)
* Kết nối mạng nội bộ giữa web và máy in
* Có thể SSH vào máy in bằng **PuTTY**

### Tải công cụ cần thiết

* **PuTTY (SSH):** [https://www.putty.org](https://www.putty.org)

---

## Cài đặt nhanh

1️⃣ **Đăng nhập vào máy in bằng PuTTY**

Mở **PuTTY**, nhập địa chỉ IP của máy in (ví dụ `192.168.1.x`), rồi nhấn **Open**.  
Tại cửa sổ terminal:
login as: pi
password: raspberry

yaml
Sao chép mã

---

2️⃣ **Kiểm tra kiến trúc CPU của máy in**

Dán lệnh sau vào PuTTY:
```bash
uname -m
Kết quả sẽ hiển thị một trong hai loại:

aarch64 → chọn bản spdbridge-aarch64-prod

armv7l → chọn bản spdbridge-armv7l-prod

3️⃣ Cài đặt Bridge tương ứng

Nếu kết quả là aarch64:

bash
Sao chép mã
wget https://raw.githubusercontent.com/seprinder/Seprinder_Bridge/master/production/spdbridge-aarch64-prod -O bridge
chmod +x bridge
sudo apt update && sudo apt install tmux -y
tmux new -s bridge ./bridge
Nếu kết quả là armv7l:

bash
Sao chép mã
wget https://raw.githubusercontent.com/seprinder/Seprinder_Bridge/master/production/spdbridge-armv7l-prod -O bridge
chmod +x bridge
sudo apt update && sudo apt install tmux -y
tmux new -s bridge ./bridge
4️⃣ Truy cập giao diện điều khiển

Mở trình duyệt và nhập địa chỉ:

cpp
Sao chép mã
http://<ip_may_in>:1122
→ Đăng nhập để cho phép website Seprinder gửi file G-code trực tiếp đến máy in Klipper.

Lưu ý
Khi đóng PuTTY, Bridge vẫn chạy vì được giữ trong tmux.
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

## Cài đặt

1️. **Đăng nhập vào máy in bằng PuTTY**

Mở **PuTTY**, nhập địa chỉ IP của máy in (ví dụ `192.168.1.x`), nhấn **Open**. Đăng nhập với tài khoản của bạn (ví dụ `pi`):

---

2️. **Kiểm tra kiến trúc CPU của máy in**

Dán lệnh sau vào PuTTY:

```bash
uname -m
```

Kết quả sẽ hiển thị một trong hai loại:

* `aarch64`  → chọn bản **spdbridge-aarch64-prod**
* `armv7l`   → chọn bản **spdbridge-armv7l-prod**

---

3️. **Tải Bridge đúng phiên bản**

**Nếu kết quả là aarch64:**

```bash
wget https://raw.githubusercontent.com/seprinder/Seprinder_Bridge/master/production/spdbridge-aarch64-prod -O bridge
chmod +x bridge
```

**Nếu kết quả là armv7l:**

```bash
wget https://raw.githubusercontent.com/seprinder/Seprinder_Bridge/master/production/spdbridge-aarch64-prod -O bridge
chmod +x bridge
```

4️. **Cài đặt tmux (nếu chưa có)**

```bash
sudo apt update
sudo apt install tmux -y
```

---

5️. **Chạy Bridge trong tmux (chạy lại mỗi lần bạn khởi động máy chủ chạy klipper)**

```bash
tmux new -s bridge "$HOME/bridge"
```

* Thoát tmux (Bridge vẫn chạy): **Ctrl + B**, sau đó **D**
* Quay lại phiên: `tmux attach -t bridge`

---

6️. **Truy cập giao diện điều khiển**

Mở trình duyệt và nhập địa chỉ:

```text
http://<ip_may_in>:1122
```

→ Đăng nhập để cho phép website Seprinder gửi file G-code trực tiếp đến máy in Klipper.

<p align="center">
  <img src="https://raw.githubusercontent.com/seprinder/Seprinder_Bridge/master/Image/huong_dan_dang_nhap.png" alt="Hướng dẫn đăng nhập Bridge (port 1122)" width="800">
</p>

---

## Lưu ý

* Khi đóng PuTTY, Bridge vẫn chạy vì được giữ trong **tmux**.

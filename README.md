#  Tự Động Hóa Máy Chủ Web và DNS trên CentOS

Tập lệnh Bash này tự động hóa việc cài đặt, cấu hình và quản lý **máy chủ web Apache** (`httpd`) và **DNS Server** (`bind`) trên hệ điều hành **CentOS**. Với giao diện menu dòng lệnh (CLI) thân thiện, người dùng có thể dễ dàng thiết lập tên miền, vùng DNS, lưu trữ web và các dịch vụ liên quan mà không cần thao tác thủ công phức tạp.

## 🚀 Tính Năng

- **Cài đặt tự động**: Cài đặt các gói phụ thuộc (`httpd`, `bind`, `bind-utils`, `epel-release`).
- **Quản lý DNS**: Tạo vùng DNS Forward và thêm bản ghi A.
- **Quản lý Web Hosting**: Thiết lập máy chủ ảo Apache với thư mục gốc tài liệu tùy chỉnh.
- **Xóa cấu hình**: Xóa máy chủ web và tùy chọn xóa thư mục gốc tài liệu.
- **Sao lưu**: Tự động sao lưu tệp cấu hình trước khi chỉnh sửa.
- **Tắt tường lửa**: Vô hiệu hóa `firewalld` để đơn giản hóa truy cập.
- **Ghi log**: Lưu nhật ký hoạt động để theo dõi các hành động.
- **Menu tương tác**: Giao diện CLI với các tùy chọn dễ sử dụng.

## 📋 Yêu Cầu

- **Hệ điều hành**: CentOS (khuyến nghị CentOS 7 hoặc 8).
- **Quyền truy cập**: Quyền `root` hoặc `sudo`.
- **Kết nối mạng**: Cần kết nối Internet để cài đặt các gói.
- **Gói phụ thuộc**: `httpd`, `bind`, `bind-utils`, `epel-release`.

## 🛠️ Hướng Dẫn Cài Đặt

1. Tạo tệp script:
   ```bash
   nano web_server.sh
   ```

2. Dán nội dung script vào `web_server.sh` bằng trình soạn thảo.

3. Cấp quyền thực thi:
   ```bash
   chmod +x web_server.sh
   ```

4. Chạy script với quyền root:
   ```bash
   sudo ./web_server.sh
   ```

> **Lưu ý**: Sử dụng tài khoản người dùng thông thường để tạo và chỉnh sửa tệp script, sau đó chuyển sang quyền `root` để chạy.

## 🖥️ Hướng Dẫn Sử Dụng

Chạy lệnh sau để khởi động script:
```bash
sudo ./web_server.sh
```

Script sẽ hiển thị menu tương tác với các tùy chọn sau:

1. **Đảm bảo cài đặt phụ thuộc**: Cài đặt các gói cần thiết (`httpd`, `bind`, `bind-utils`, `epel-release`).
2. **Thêm tên miền và vùng DNS**:
   - Nhập tên miền (ví dụ: `example.com`) và địa chỉ IP (ví dụ: `192.168.1.10`).
   - Tạo tệp vùng DNS Forward và cập nhật `/etc/named.rfc1912.zones`.
3. **Thêm hosting cho tên miền**:
   - Thiết lập máy chủ ảo Apache với thư mục gốc tài liệu (`/var/www/html/<tên-miền>`).
   - Tạo tệp `index.html` mặc định nếu chưa tồn tại.
4. **Liệt kê các tên miền đang hoạt động**: Hiển thị danh sách các tên miền được cấu hình trong Apache.
5. **Xóa máy chủ web**:
   - Xóa tệp cấu hình Apache và tùy chọn xóa thư mục gốc tài liệu.
   - Sao lưu tệp cấu hình trước khi xóa.
6. **Tắt tường lửa**: Dừng và vô hiệu hóa dịch vụ `firewalld`.
7. **Thoát**: Thoát khỏi script.

### Ví dụ Sử Dụng

- **Thêm tên miền**:
  - Chọn tùy chọn 2, nhập `example.com` và IP `192.168.1.10`.
  - Kết quả: Tệp vùng DNS `/var/named/forward.example.com` được tạo và `/etc/named.rfc1912.zones` được cập nhật.

- **Thêm hosting**:
  - Chọn tùy chọn 3, nhập `example.com` và thư mục (mặc định là `example.com`).
  - Kết quả: Tệp cấu hình `/etc/httpd/conf.d/example.com.conf` và thư mục `/var/www/html/example.com` được tạo.

- **Kiểm tra tên miền**:
  - Chọn tùy chọn 4 để liệt kê các tên miền đang hoạt động.

## 📂 Cấu Trúc Thư Mục

```
/var/www/html/<tên-miền>            # Thư mục gốc tài liệu cho tên miền
/etc/httpd/conf.d/<tên-miền>.conf   # Tệp cấu hình máy chủ ảo Apache
/var/named/forward.<tên-miền>       # Tệp vùng DNS Forward
/etc/named.rfc1912.zones            # Tệp cấu hình vùng DNS
/var/log/autoscript.log             # Nhật ký hoạt động của script
```


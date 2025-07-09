## 🐧 Linux

| File mục tiêu                  | Chức năng / Thông tin nhạy cảm                      |
|-------------------------------|-----------------------------------------------------|
| `/etc/passwd`                 | Danh sách người dùng hệ thống                      |
| `/etc/shadow`                 | Mật khẩu đã mã hóa (chỉ root đọc được)             |
| `/etc/hosts`                  | Cấu hình ánh xạ tên miền cục bộ                    |
| `/proc/self/environ`          | Biến môi trường, có thể chứa `FLAG`, `API_KEY`,... |
| `/var/log/apache2/access.log` | Log truy cập web, có thể chứa payload trước đó     |
| `/var/log/apache2/error.log`  | Log lỗi PHP, debug thông tin nhạy cảm              |
| `/home/username/.ssh/id_rsa`  | Private key SSH người dùng                         |
| `.env`                        | File cấu hình chứa mật khẩu DB, API key,...        |
| `config.php`, `wp-config.php` | Thường chứa thông tin kết nối CSDL                 |

## 🪟 Windows

| File mục tiêu                          | Chức năng / Thông tin nhạy cảm                      |
|----------------------------------------|-----------------------------------------------------|
| `C:\\Windows\\System32\\drivers\\etc\\hosts` | Cấu hình ánh xạ tên miền                           |
| `C:\\Windows\\win.ini`                 | Cấu hình hệ thống cũ                               |
| `C:\\boot.ini`                         | Cấu hình boot Windows (Windows cũ)                 |
| `C:\\Windows\\System32\\config\\SAM`   | Chứa hash mật khẩu user (chỉ SYSTEM đọc được)     |
| `C:\\Windows\\System32\\config\\system`| Cấu hình hệ thống registry                         |
| `web.config`                           | Cấu hình ứng dụng ASP.NET, chứa chuỗi kết nối DB   |
| `.env`                                 | (nếu có) chứa thông tin nhạy cảm trong project     |
| `php.ini`                              | Cấu hình PHP – xác định thư mục upload, temp,...   |

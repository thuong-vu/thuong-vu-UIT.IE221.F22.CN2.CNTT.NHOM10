

```markdown
# Sổ Thu Chi — Ứng dụng quản lý thu chi cá nhân

Flask + MySQL + HTML/CSS/JS thuần · Mobile-first SPA

## Cài đặt & Chạy

### 1. Khởi động MySQL Server
Đảm bảo dịch vụ MySQL Server trên máy của bạn đang hoạt động (có thể chạy qua Service của HĐH, Docker, hoặc các phần mềm quản lý như MySQL Workbench).

### 2. Tạo database
- Sử dụng giao diện dòng lệnh (CLI) của MySQL hoặc các công cụ quản lý CSDL (như DBeaver, MySQL Workbench).
- Nếu dùng CLI, mở Terminal tại thư mục gốc của dự án và chạy lệnh sau (nhập mật khẩu nếu được yêu cầu):
```bash
mysql -u root -p < database/thu_chi_db.sql

```

*(Lưu ý: File này đã bao gồm lệnh tạo database `thu_chi_db`, tạo bảng và thiết lập Trigger sinh danh mục mặc định).*

### 3. Cấu hình môi trường

* Mở file `db.py`.
* Chỉnh sửa thông số `'user': '...'` và `'password': '...'` cho khớp với tài khoản MySQL trên máy của bạn.

### 4. Cài Python dependencies

```bash
pip install flask pymysql dbutils werkzeug

```

*(Hoặc chạy `pip install -r requirements.txt` nếu bạn có file cấu hình thư viện).*

### 5. Chạy ứng dụng

```bash
python app.py

```

### 6. Mở trình duyệt

Truy cập vào địa chỉ:

```text
http://localhost:5000

```

---

## Cấu trúc dự án

```text
thu-chi-app/
├── app.py              Flask app + API Thu/Chi và Thống kê
├── auth.py             Flask Blueprint xử lý Đăng ký/Đăng nhập và Session
├── db.py               Hàm get_connection() dùng PyMySQL và Connection Pool
├── requirements.txt    (Tuỳ chọn) Chứa danh sách thư viện Python
├── database/
│   └── thu_chi_db.sql  File khởi tạo CSDL + bảng + Trigger (chạy 1 lần)
└── templates/
    ├── index.html      Toàn bộ UI chính (Dashboard Single-page)
    └── auth.html       UI Đăng nhập và Đăng ký

```

## API Endpoints

| Method | URL                                             | Mô tả                                      |
| ---    | ----------------------------------------------- | ------------------------------------------ |
| POST   | `/api/auth/register`                            | Đăng ký tài khoản mới                      |
| POST   | `/api/auth/login`                               | Đăng nhập (tạo session)                    |
| POST   | `/api/auth/logout`                              | Đăng xuất (xóa session)                    |
| GET    | `/api/auth/me`                                  | Kiểm tra trạng thái đăng nhập              |
| GET    | `/api/overview`                                 | Tổng quan tháng này + 5 giao dịch gần nhất |
| GET    | `/api/transactions?month=YYYY-MM&category_id=N` | Danh sách giao dịch                        |
| POST   | `/api/transactions`                             | Thêm giao dịch mới                         |
| DELETE | `/api/transactions/:id`                         | Xoá giao dịch                              |
| GET    | `/api/stats?period=week|month|year`             | Thống kê tổng thu/chi + phân tích danh mục |
| GET    | `/api/categories`                               | Danh sách danh mục                         |
| POST   | `/api/categories`                               | Thêm danh mục cá nhân mới                  |
| DELETE | `/api/categories/:id`                           | Xóa danh mục cá nhân                       |

## Yêu cầu hệ thống

* Python 3.9+
* MySQL 5.7+ / MariaDB 10.4+
* Trình duyệt hiện đại (Chrome, Firefox, Safari, Edge)

```

```

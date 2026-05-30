# PT_UNGDUNG_MANGUON
### Nguyễn Thị Thu Hiền: K225480106015
## SỬ DỤNG WORDPRESS ĐỂ TẠO WEB SITE
deadline : 23h59 ngày 12 tháng 5 năm 2026.
### Đề bài:
1. SỬ DỤNG DOCKER TRÊN UBUNTU ĐỂ TẠO docker ccompose chứa:

Mariadb: sử dụng image: mariadb:latest để làm hệ quản trị csdl cho wordpress

Phpmyadmin: sư dụng image: phpmyadmin:latest để đăng nhập vào mariadb rồi tạo csdl trống (chỉ để xem, ko cần tạo bảng từ đây, wordpress sẽ làm hết)

WordPress: Sử dụng image: wordpress:latest, truyền các tham số môi trường cho wordpress là các thông tin truy cập csdl mariadb, tạo bởi Phpmyadmin

2. Yêu cầu: sau khi có 3 service này trong file docker-compose.yml :

Cấu hình để hệ thống chạy

Sử dụng cloudflare tunnel để public web này lên 1 sub-domain

Tạo 1 bài viết trong wordpress giới thiệu về bản thân sinh viên: thông tin cá nhân, sở thích, ... bài viết có thể chứa hình ảnh, âm thanh, video, ...

Tạo 1 bài viết trong wordpress giới thiệu về ngành học mà em yêu thích trong trường TNUT. bài viết phải chứa hình ảnh, video, ...

Nhận xét việc sử dụng mã nguồn mở wordpress để tạo website (tốn công sức thế nào, dễ/khó dùng ra sao, tốn kém tài nguyên(ssh/ram) của máy chủ ra sao,....)

------------------------------------------------------------------------------------------------------------------------------------------------------------
### BÀI LÀM
1. SỬ DỤNG DOCKER TRÊN UBUNTU ĐỂ TẠO docker ccompose chứa:
- Trước tiên, vào Ubuntu và nhập các lệnh để khởi tạo các thư mục project, ở đây e đặt tên project là " wordpress":
<img width="614" height="219" alt="image" src="https://github.com/user-attachments/assets/8d53f66f-4304-4cc8-a047-0638c37e9cfd" />

- Sửa file docker-compose.yml, có thêm 3 service: Mariadb: sử dụng image: mariadb:latest để làm hệ quản trị csdl cho wordpress, Phpmyadmin: sư dụng image: phpmyadmin:latest để đăng nhập vào mariadb rồi tạo csdl trống (chỉ để xem, ko cần tạo bảng từ đây, wordpress sẽ làm hết), WordPress: Sử dụng image: wordpress:latest, truyền các tham số môi trường cho wordpress là các thông tin truy cập csdl mariadb, tạo bởi Phpmyadmin
<img width="961" height="950" alt="image" src="https://github.com/user-attachments/assets/fc1cf3a7-b017-4014-a1d2-460492c9bcbe" />

- Sau đó chạy file docker, để cả 3 container kia chạy. Ở đây :
+ wordpress-db-1 = MariaDB chứa CSDL
+ wordpress-phpmyadmin-1 = giao diện xem CSDL qua trình duyệt
+ wordpress-wordpress-1 = website WordPress
<img width="948" height="362" alt="image" src="https://github.com/user-attachments/assets/ef2cf506-3096-4997-9f68-23b65b2d28b4" />

- Tiếp theo, mở trình duyệt chạy localhost `http://localhost:8090` để cài đặt Wordpress và ` http://localhost:8082` để PHPMyadmin xem cơ sở dữ liệu:
<img width="1789" height="1021" alt="image" src="https://github.com/user-attachments/assets/84ae5b5b-dd91-4ede-b6ff-569d0a9d1801" />


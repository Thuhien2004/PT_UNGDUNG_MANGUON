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
+ Trước tiên chạy cài đặt Wordpress, vào chọn ngôn ngữ và điền thông tin vào các mục:
<img width="1789" height="1021" alt="image" src="https://github.com/user-attachments/assets/84ae5b5b-dd91-4ede-b6ff-569d0a9d1801" />
<img width="1162" height="724" alt="image" src="https://github.com/user-attachments/assets/9b6785ad-3df6-44d9-917a-9fe493032f58" />

+ Sau khi chọn cài đặt wordpress, màn hình hiện ra giao diện đăng nhập, nhập tên đăng nhập và mật khẩu để vào trang quản lý:
<img width="1917" height="1031" alt="image" src="https://github.com/user-attachments/assets/3f8e4c35-6543-4aa0-b5f5-866147892f30" />

-  Giờ là bước cài tunnel:
+ Truy cập trang cloudflare zero trust, tạo một tunnel mới.
<img width="1905" height="922" alt="image" src="https://github.com/user-attachments/assets/23ed1eb4-576a-4581-826b-9466e92e5efa" />
<img width="1912" height="708" alt="image" src="https://github.com/user-attachments/assets/db0ea1af-6049-494f-bf37-c956e7de6e17" />

+ Sau khi coppy dòng lệnh, thì paste vào terminal ubuntu, sau đó chọn next trong giao diện cloudflare mà đang hiện các lệnh copy. Rồi cài đặt route:
<img width="1191" height="809" alt="image" src="https://github.com/user-attachments/assets/7eec9d91-c212-4112-9f14-09a9d7f3a445" />
<img width="1627" height="261" alt="image" src="https://github.com/user-attachments/assets/40f0199f-e7f7-4f67-aeef-4b8f0fb5a94f" />

+ Sau đó truy cập địa chỉ: https://wordpress.thuhien2004.io.vn ở trên trình duyệt. Lúc này, bị lỗi ko thể truy cập, kiểm tra DNS record.
<img width="920" height="770" alt="image" src="https://github.com/user-attachments/assets/939dc280-fb7a-47c7-b45a-4c4406b64966" />
+ Vào dash.cloudflare.com → thuhien2004.io.vn → DNS → Records . Nếu thấy có DNS rồi, thì vào lại trang chủ admin wordpress -> vào cài đặt chung rồi, nhập địa chỉ Url theo tunnel đã tạo:
<img width="1916" height="969" alt="image" src="https://github.com/user-attachments/assets/4cabf4c6-28d6-4091-9984-b7c57ef2125b" />



# BÀI TẬP SỐ 5
  - lý thuyết: 
    + docker là gì? 
    + các keyword được sử dụng trong docker-compose.yml
      để mô tả 1 service, network, volume,...
      liệt kê + ý nghĩa của từ khoá đó + ví dụ minh hoạ
    + ưu điểm khi triển app sử dụng docker là gì?
    + dùng docker: tạo app, test app OK trên laptop cá nhân
      giờ muốn triển khai app này trên máy chủ thật ko có internet
      thì các bước cần làm là?
  - thực hành áp dụng: APP MONITOR + ALERT DATA REALTIME
    sử dụng docker compose có nhiều serivce 
    và các thành phần cần thiết để tạo thành ứng dụng:
     + nodered liên tục lấy dữ liệu từ nguồn nào đó (chứng khoán, thời tiết, giá vàng,...)
       nguồn thực tế, số liệu luôn động sau thời gian ngắn
     + nodered lưu trữ dữ liệu vào 2 database: mariadb để lưu giá trị tức thời
       lưu lịch sử vào influxdb
     + sử dụng grafana để trực quan hoá dữ liệu: vẽ biểu đồ
     + sử dụng nginx để làm webserver
       chạy 1 trang web html+js+css làm front-end
       js: lấy dữ liệu tức thời trong mariadb qua (ajax | socket) 
           gọi api (api tự build bằng Flask giống bt1)
           api trả về giá trị tức thời trong mariadb
           hiển thị lên web, auto hiển thị số mới khi thay đổi
       sử dụng iframe để gọi grafana
       hiển thị biểu đồ dữ liệu lịch sử của thông số đã lưu
     + QUAN SÁT DỮ LIỆU LỊCH SỬ => GIÁ TRỊ BẤT THƯỜNG
       (VD MIỀN A..B: OK, DƯỚI A: ALERT LOW, TRÊN B: ALERT HIGH)
     + nodered: kết hợp bot Telegram
       khi dữ liệu not OK, thì gửi tin nhắn từ bot => group trên telegram
       group đã add bot vào: (nhóm đã có 2 người), add thêm 1875746636 thành 3 người
       mỗi khi bot gửi dữ liệu vào nhóm: mọi member of group đều nhận đc
       nội dung alert: tường minh, có value gây alert
     xuất tất cả các container ra file nén.
     xoá mọi container đang chạy
     load lại các container  từ file nén để khôi phục các container đã xoá
----------------------------------------------------------------------------------------------
# BÀI LÀM
### 1. Docker là gì?
- Docker là một nền tảng mã nguồn mở cho phép các nhà phát triển tự động đóng gói ứng dụng cùng với toàn bộ các thành phần phụ thuộc đi kèm (như mã nguồn, thư viện, môi trường chạy, cấu hình hệ thống) vào trong một đơn vị duy nhất gọi là Container.
- Cơ chế hoạt động: Container chạy hoàn toàn độc lập và cô lập với hệ điều hành máy chủ (Host OS). Khác với công nghệ ảo hóa truyền thống (Virtual Machine - VM) yêu cầu tích hợp một hệ điều hành khách (Guest OS) nặng nề và chiếm dụng nhiều tài nguyên phần cứng, Docker Container chia sẻ chung nhân (Kernel) của hệ điều hành máy chủ.
- Kết quả: Nhờ chia sẻ nhân, các container cực kỳ nhẹ (khởi động tính bằng giây thay vì bằng phút như VM) và đảm bảo ứng dụng luôn chạy đồng nhất trên mọi môi trường (từ máy tính cá nhân của lập trình viên cho đến máy chủ production thật).
### 2. Các từ khóa (Keywords) sử dụng trong docker-compose.yml
- File docker-compose.yml sử dụng ngôn ngữ định dạng YAML để định nghĩa, cấu hình và quản lý một ứng dụng gồm tổ hợp nhiều dịch vụ (Multi-container). Dưới đây là các từ khóa cốt lõi dùng để mô tả một service, network, volume cùng ý nghĩa và ví dụ cụ thể:
+ version: 	Khai báo phiên bản cú pháp cấu hình của Docker Compose để hệ thống hiểu và hỗ trợ các tính năng tương ứng:	version: '3.8'
+ services	Từ khóa gốc cấp cao nhất, khai báo bắt đầu danh sách các container dịch vụ độc lập sẽ được tạo.	services app_mariadb:
+ image	: Chỉ định tên và phiên bản Docker Image tải về từ Docker Hub để làm phôi chạy container: 	image: mariadb:10.6
+ build:	Chỉ định đường dẫn tới thư mục chứa file Dockerfile để tự động build image mới thay vì tải từ mạng.	build: ./api
+ container_name:	Định danh tên cố định cho container, giúp dễ dàng kiểm tra trạng thái và log bằng lệnh CLI.	container_name: monitor_db
+ ports:	Ánh xạ cổng từ máy vật lý (Host) vào container theo cú pháp: "MÁY_THẬT:CONTAINER".	ports: "3306:3306"
+ expose	: Chỉ mở cổng nội bộ cho các container khác trong cùng mạng gọi nhau, không mở ra ngoài máy thật (bảo mật cao).	expose: "3306"
+ environment:	Thiết lập các biến môi trường trực tiếp bên trong container (như tài khoản, mật khẩu, thông số kỹ thuật).	environment MYSQL_ROOT_PASSWORD: admin
+ env_file:	Nạp một danh sách dài các biến môi trường từ một file ẩn .env bên ngoài vào hệ thống cho gọn và bảo mật:	env_file.env
 + volumes:	Gắn ổ đĩa từ máy thật vào container để lưu trữ dữ liệu vĩnh viễn, tránh mất data khi khởi động lại:	volumes db_data:/var/lib/mysql
+ networks:	Tạo mạng nội bộ ảo cho cụm container giao tiếp bảo mật với nhau thông qua tên dịch vụ:	networks monitor_net
+ depends_on:Thiết lập thứ tự khởi chạy. Container B chỉ chạy khi container A làm nền tảng đã khởi động xong.	depends_on  mariadb
+ restart:Cấu hình tự động khởi động lại container nếu bị lỗi sập hoặc khi máy chủ vừa khởi động lại.	restart: always(hoặc: unless-stopped)
+ command:	Ghi đè (override) câu lệnh chạy mặc định của image gốc bằng một câu lệnh thực thi mới khi khởi động.	command: python app.py
+ healthcheck:	Thiết lập bài kiểm tra định kỳ để xem container có đang hoạt động khỏe mạnh hay bị treo ngầm.	healthcheck:test: ["CMD", "curl", "-f","http://localhost"] logging
+ Cấu hình giới hạn dung lượng file log để tránh tình trạng rác log làm đầy ổ cứng của máy chủ.	logging options max-size: "10m"
### 3. Ưu điểm khi sử dụng docker compose
Đây là nội dung chi tiết trả lời cho câu hỏi về ưu điểm khi triển khai ứng dụng (deploy app) bằng Docker. Triển khai ứng dụng bằng Docker mang lại sự đột phá so với các phương pháp cài đặt vật lý (Bare-metal) hay máy ảo (Virtual Machine) truyền thống. Dưới đây là 5 ưu điểm cốt lõi:
1. Tính nhất quán tuyệt đối (Đồng nhất môi trường)
-	Bản chất: Docker đóng gói code và mọi thư viện, cấu hình đi kèm vào một khối duy nhất.
-	Ưu điểm: Với Docker, môi trường bên trong container là cố định. Bạn mang container đó chạy trên Laptop, máy chủ nội bộ hay Cloud thì nó đều hoạt động y hệt nhau 100%.
2. Tiết kiệm tối đa tài nguyên phần cứng
-	Bản chất: Khác với máy ảo (VM) phải vác theo cả một Hệ điều hành khách (Guest OS) nặng hàng chục GB, các Docker container chia sẻ chung nhân (Kernel) của hệ điều hành máy chủ.
-	Ưu điểm: Container cực kỳ nhẹ (chỉ tốn vài chục MB). Có thể chạy hàng chục, thậm chí hàng trăm dịch vụ (services) trên cùng một máy chủ VPS cấu hình thấp mà không lo bị ngốn cạn RAM hay CPU.
3. Khởi động và triển khai siêu tốc
-	Bản chất: Vì không phải khởi động một hệ điều hành mới như máy ảo, container thực chất chỉ là một tiến trình (process) chạy trên máy chủ.
-	Ưu điểm: Thời gian tạo mới, khởi động, tắt hoặc khởi động lại (restart) hệ thống chỉ tính bằng giây. Điều này giúp việc cập nhật phiên bản mới (Update/Patch) hoặc khôi phục hệ thống khi có sự cố diễn ra chớp nhoáng.
4. Tính cô lập an toàn (Isolation & Security)
-	Bản chất: Mỗi container hoạt động trong một ranh giới khép kín độc lập.
-	Ưu điểm: Các ứng dụng không bị xung đột với nhau (Ví dụ: Bạn có thể chạy cùng lúc 2 web dùng PHP 5 và PHP 8 trên cùng 1 máy chủ mà không bị lỗi). Ngoài ra, nếu một container bị hacker tấn công hoặc bị lỗi tràn RAM, nó cũng không thể lây lan làm sập các container khác hay sập hệ điều hành gốc của máy chủ.
5. Hỗ trợ tuyệt vời cho Mở rộng (Scalability) và Tự động hóa (CI/CD)
-	Bản chất: Việc cấu hình hạ tầng được viết thành code (thông qua file docker-compose.yml hoặc Dockerfile).
-	Ưu điểm: Khi lượng người dùng tăng đột biến, quản trị viên chỉ cần gõ 1 dòng lệnh là có thể nhân bản (scale) từ 1 container lên 10 container để gánh tải ngay lập tức. Đây là nền tảng bắt buộc để xây dựng kiến trúc Microservices hiện đại.

 ### 4. Triển khai app bằng docker trên máy chủ khi không có Internet
Giai đoạn 1: Chuẩn bị và xuất dữ liệu (Tại Laptop cá nhân có Internet)
-	Kéo (pull) hoặc tự build đầy đủ các Docker Image cần thiết cho hệ thống (ví dụ: Node-RED, MariaDB, Nginx...).
-	Sử dụng lệnh nén docker save để xuất các image đang có trong máy thành các tệp tin vật lý định dạng .tar.
-	Cú pháp lệnh: docker save -o <tên_file_nén.tar> <tên_image_gốc>
-	Tập hợp tất cả các file .tar vừa xuất cùng với file cấu hình docker-compose.yml (và các thư mục volume/source code nếu có) vào chung một thư mục.
Giai đoạn 2: Vận chuyển dữ liệu (Thao tác vật lý)
-	Sao chép thư mục tổng hợp ở Giai đoạn 1 vào một thiết bị lưu trữ ngoại vi như USB hoặc Ổ cứng di động.
-	Mang thiết bị lưu trữ này cắm trực tiếp vào máy chủ thực tế (Production Server) đang bị cô lập mạng (Offline).
Giai đoạn 3: Phục hồi và khởi chạy (Tại Máy chủ Offline)
-	Sao chép toàn bộ dữ liệu từ USB vào ổ cứng của máy chủ.
-	Sử dụng lệnh docker load để giải nén và nạp các file .tar vào kho quản lý Image nội bộ của Docker trên máy chủ.
-	Cú pháp lệnh: docker load -i <tên_file_nén.tar>
-	Sử dụng lệnh docker images để kiểm tra lại, đảm bảo toàn bộ image đã được nạp thành công vào hệ thống.
-	Mở Terminal (hoặc CMD), di chuyển (cd) vào đúng thư mục đang chứa file docker-compose.yml.
-	Thực thi lệnh docker-compose up -d để Docker tự động đọc cấu hình và khởi chạy toàn bộ hệ thống ngầm định mà không cần kết nối Internet



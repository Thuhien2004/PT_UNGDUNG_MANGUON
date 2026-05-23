Môn: Phát triển ứng dụng với mã nguồn mở-TEE0421

Lớp: 58KTPM

Họ và tên: Nguyễn Thị Thu Hiền

MSSV: K225480106015

# SỬ DỤNG DJANGO ĐỂ TẠO WEB QUẢN LÝ TIỆM CẦM ĐỒ
### deadline : 23h59 ngày 09 tháng 5 năm 2026
---------------------------------------------------------------------------------
1. TỔ CHỨC CSDL CHO HỆ THỐNG QUẢN LÝ TIỆM CẦM ĐỒ:
viết tay ra giấy, lấy điện thoại chụp lại, upload ảnh lên github (đã nói về các nghiệp vụ trên lớp, ghi bảng)
2. SỬ DỤNG DOCKER TRÊN UBUNTU ĐỂ:
- Mariadb : chứa csdl của hệ thống này
- Phpmyadmin: để soi được csdl (chỉ để xem, ko cần tạo bảng từ đây, django sẽ làm hết)
- Django: build 1 docker container (dùng Dockerfile): trên nền python, sử dụng django, nhớ mount thư mục để dễ edit, edit dùng: sudo nano ten_file
sau khi có 3 service này trong file docker-compose.yml :
- run nó, cấu hình để Django nhận csdl mariadb (sửa file settings.py), cấu hình user login ban đầu, mô tả các bảng trong models.py, .... (đc phép sử dụng AI để làm) => KQ được trang admin, y/c đăng nhập, vào trang admin: cho phép thêm sửa xoá dữ liệu các bảng. các trường là khoá ngoại chỉ việc chọn text (mặc dù là csdl tại trường FK đó lưu ID của PK mà nó tham chiếu : sử dụng phpmyadmin để kiểm chứng)
- chú ý kết hợp ssh để chạy lệnh tác động vào django và sudo nano để edit file.
- sử dụng template (file html, sử dụng cú pháp jinja2), lấy context từ 1 view home_page, để tạo trang liệt kê các con nợ đến hạn mà chưa trả tiền!
- sử dụng cloudflare tunnel để public kết quả lên 1 sub-domain => chụp kết quả
Hướng dẫn:
- Tạo thư mục để chứa image tự buid cho django
- Vào thư mục đó tạo file tên: Dockerfile (nội dung hỏi AI xem file này cần có nội dung gì, full comment cho từng dòng lệnh trong file này => mục tiêu kép: để hiểu và để hệ thống chạy được)
- AI sẽ nói cần thêm file requirements.txt để cài các thư viện cho python (cài qua lệnh pip) => tạo file requirements.txt với nội dung tưng ứng, trong file này cũng comment được => comment xem thư viện nào dùng để làm gì
- Sau mỗi lần sửa đỏi có thể phải chạy lệnh dạng : docker compose exec TÊN_SERVICE_DJANGO_CỦA_BẠN python manage.py migrate để tác động vào django (còn nhiều lệnh khác chứ ko luôn như này), để django thay đổi csdl hoặc thay đổi cấu hình.
- -------------------------------------------------------------------------------------------
  -----------------------------------------------------------------------------------------
  # BÀI LÀM
  1.  TỔ CHỨC CSDL CHO HỆ THỐNG QUẢN LÝ TIỆM CẦM ĐỒ:

<img width="1920" height="2560" alt="image" src="https://github.com/user-attachments/assets/fdc6d318-db9c-41d3-b1bd-34f65b7bbc8c" />

2. SỬ DỤNG DOCKER TRÊN UBUNTU
Trước hết thì: Em thấy ubuntu trên VMware của em nó bị lỗi mà em chưa thể sửa được. Nên em dùng WSL+ubuntu
<img width="638" height="424" alt="image" src="https://github.com/user-attachments/assets/0f54621c-1dbf-4384-96a1-a9743b4463de" />

- Tạo project cho bài , xong tại cấu trúc thư mục.
<img width="956" height="730" alt="image" src="https://github.com/user-attachments/assets/9acdaa1b-1173-4001-9b62-eda3ce8707e6" />

- Tạo file Dockerfile:
<img width="955" height="335" alt="image" src="https://github.com/user-attachments/assets/032780d2-f7d3-4c2b-99a4-d4ff584ade2d" />

- Tạo file requirement.txt
<img width="927" height="198" alt="image" src="https://github.com/user-attachments/assets/bbf0d10d-7cda-4d7f-8788-9f56e57f4db8" />
<img width="945" height="910" alt="image" src="https://github.com/user-attachments/assets/b9fd08ce-4640-498a-a4e9-bdffd52316a6" />

- Tạo file Docker-compose.yml
<img width="959" height="825" alt="image" src="https://github.com/user-attachments/assets/0a34a6bb-c756-42ac-a139-8984e89f80ea" />

- Build và chạy docker bằng cú pháp : ''docker compose up -d --build'' , rồi chờ vài phút để tải Image về
<img width="942" height="251" alt="image" src="https://github.com/user-attachments/assets/e531ab73-ac3a-46a0-bea1-fefb54727e9f" />
<img width="944" height="154" alt="image" src="https://github.com/user-attachments/assets/35427a47-7444-40e8-b66a-884216e78fc0" />

- Tạo app 'core' trong Django:
<img width="955" height="200" alt="image" src="https://github.com/user-attachments/assets/f2d67b9d-8750-436f-88f3-fc8a3f32bba4" />

 - Sửa file setting.py để kết nối MariaDB:
- Vì dùng PyMySQL nên phải sửa thêm file --init__.py của project
<img width="943" height="278" alt="image" src="https://github.com/user-attachments/assets/f64dacb0-db24-4604-9549-be9508c2a2ed" />

- Tạo tài khoản admin để đăng nhập:
<img width="1919" height="875" alt="image" src="https://github.com/user-attachments/assets/bd5f0cd4-2b59-4c3f-b700-a109fe6e3b3f" />

- Sau đó vào trình duyệt chạy localhost , đăng nhập bằng tài khoản vừa tạo trước đó:
<img width="1919" height="765" alt="image" src="https://github.com/user-attachments/assets/d1c861d8-ff25-4508-8ef5-af17eae441c5" />
<img width="959" height="1014" alt="image" src="https://github.com/user-attachments/assets/8652b291-f643-40ca-b936-3f7cde4b392c" />

- Trang admin đã chạy, sau đó tiếp tục đưa cơ sở dữ liệu vào trang bằng cách tạo models.py:
<img width="954" height="433" alt="image" src="https://github.com/user-attachments/assets/898613b6-8567-457d-ae8c-293d6b4d1c45" />

'''
from django.db import models

class KhachHang(models.Model):

    ho_ten = models.CharField(max_length=100, verbose_name="Họ tên")
    
    so_dien_thoai = models.CharField(max_length=15, verbose_name="SĐT")
    
    dia_chi = models.TextField(blank=True, verbose_name="Địa chỉ")
    
    cmnd = models.CharField(max_length=20, unique=True, verbose_name="CMND/CCCD")

    def __str__(self):
        return f"{self.ho_ten} ({self.cmnd})"

    class Meta:
        verbose_name = "Khách hàng"
        verbose_name_plural = "Khách hàng"


class TaiSan(models.Model):

    ten_tai_san = models.CharField(max_length=200, verbose_name="Tên tài sản")
    
    mo_ta = models.TextField(blank=True, verbose_name="Mô tả")

    def __str__(self):
        return self.ten_tai_san

    class Meta:
    
        verbose_name = "Tài sản"
        
        verbose_name_plural = "Tài sản"


class HopDongCamDo(models.Model):

    TRANG_THAI_CHOICES = [
        ('dang_cam', 'Đang cầm'),
        ('da_chuoc', 'Đã chuộc'),
        ('qua_han', 'Quá hạn'),
    ]
    khach_hang = models.ForeignKey(
        KhachHang, on_delete=models.CASCADE,
        verbose_name="Khách hàng"
    )
    tai_san = models.ForeignKey(
        TaiSan, on_delete=models.CASCADE,
        verbose_name="Tài sản cầm"
    )
    so_tien_cam = models.DecimalField(
        max_digits=15, decimal_places=0,
        verbose_name="Số tiền cầm (VNĐ)"
    )
    lai_suat = models.DecimalField(
        max_digits=5, decimal_places=2,
        default=3.0, verbose_name="Lãi suất (%/tháng)"
    )
    ngay_cam = models.DateField(verbose_name="Ngày cầm")
    ngay_dao_han = models.DateField(verbose_name="Ngày đáo hạn")
    trang_thai = models.CharField(
        max_length=20, choices=TRANG_THAI_CHOICES,
        default='dang_cam', verbose_name="Trạng thái"
    )
    ghi_chu = models.TextField(blank=True, verbose_name="Ghi chú")

    def __str__(self):
        return f"HĐ #{self.id} - {self.khach_hang} - {self.ngay_dao_han}"

    class Meta:
        verbose_name = "Hợp đồng cầm đồ"
        verbose_name_plural = "Hợp đồng cầm đồ"


class ThanhToan(models.Model):

    hop_dong = models.ForeignKey(
        HopDongCamDo, on_delete=models.CASCADE,
        verbose_name="Hợp đồng"
    )
    ngay_thanh_toan = models.DateField(verbose_name="Ngày thanh toán")
    so_tien = models.DecimalField(
        max_digits=15, decimal_places=0,
        verbose_name="Số tiền (VNĐ)"
    )
    ghi_chu = models.TextField(blank=True, verbose_name="Ghi chú")

    def __str__(self):
        return f"TT HĐ #{self.hop_dong.id} - {self.ngay_thanh_toan}"

    class Meta:
    
        verbose_name = "Thanh toán"
        verbose_name_plural = "Thanh toán" 
        '''

- Tạo bảng trong CSDL:
<img width="1854" height="710" alt="image" src="https://github.com/user-attachments/assets/8161ad9e-7b07-4b7e-bf28-a1364731d0f2" />

- Tiếp theo , đăng ký các bảng vào trang admin , sửa file admin.py

from django.contrib import admin

from .models import KhachHang, TaiSan, HopDongCamDo, ThanhToan

@admin.register(KhachHang)

class KhachHangAdmin(admin.ModelAdmin):

    list_display = ['ho_ten', 'cmnd', 'so_dien_thoai', 'dia_chi']
    
    search_fields = ['ho_ten', 'cmnd']

@admin.register(TaiSan)

class TaiSanAdmin(admin.ModelAdmin):

    list_display = ['ten_tai_san', 'mo_ta']

@admin.register(HopDongCamDo)

class HopDongCamDoAdmin(admin.ModelAdmin):

    list_display = ['id', 'khach_hang', 'tai_san', 'so_tien_cam', 'ngay_dao_han', 'trang_thai']
    
    list_filter = ['trang_thai']
    
    search_fields = ['khach_hang__ho_ten']

@admin.register(ThanhToan)

class ThanhToanAdmin(admin.ModelAdmin):

    list_display = ['hop_dong', 'ngay_thanh_toan', 'so_tien']

- Sau đó restart lại Django và mở lại địa chỉ localhost:
![Uploading image.png…]()

+ Trang admin đã có đủ các bảng , bây giờ ta sẽ thêm dữ liệu mẫu vào để test:
  
1. Click Khách hàng → Thêm vào → nhập thông tin → Lưu

2. Click Tài sản → Thêm vào → nhập tên tài sản → Lưu

3. Click Hợp đồng cầm đồ → Thêm vào → chọn khách hàng, tài sản từ dropdown → nhập ngày đáo hạn là ngày hôm qua → Lưu



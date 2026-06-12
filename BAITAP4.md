Tiếp tục từ bài tập số 3, các container từ bài tập 3 đảm bảo vẫn tồn tại để tiếp tục thao tác. Ta sẽ thêm service n8n vào file docker-compose.yml, edit file config.yml và pull image:
 
<img width="979" height="508" alt="image" src="https://github.com/user-attachments/assets/e18467d9-32e1-413b-8ecc-f933e97c29ed" />
<img width="955" height="428" alt="image" src="https://github.com/user-attachments/assets/cb5e5a54-c34e-4752-98eb-b4a4682df9c9" />
<img width="979" height="188" alt="image" src="https://github.com/user-attachments/assets/7f3f71b7-459f-4960-aea1-4a5c21691f58" />

Sau đó ta truy cập Cloudflare cá nhân, vào mục domain -> DNS record kiểm tra xem đã có 3 public host name chưa, nếu có thì đã được thêm vào.  
<img width="862" height="401" alt="image" src="https://github.com/user-attachments/assets/5f1f3379-99c3-4c7f-973c-a5414561dd15" />
<img width="979" height="106" alt="image" src="https://github.com/user-attachments/assets/68824dc2-dc3e-4209-9894-a0e8bf2bb65c" />
<img width="964" height="504" alt="image" src="https://github.com/user-attachments/assets/88187e75-6900-411b-8a01-37d396be82ab" />
<img width="979" height="521" alt="image" src="https://github.com/user-attachments/assets/b3973283-1115-4be7-817a-639339842941" />

Tiếp theo tạo một con BOT telegram mới , mở ứng dụng Telegram trên điện thoại hoặc máy tính lên, tìm kiếm người dùng tên là @BotFather (có tích xanh chính chủ). Tạo newbot và lưu lại http API token , tìm kiếm @userinfobot để lấy id máy chủ. Và truy cập vào trang Google studio để lấy API key. 
<img width="979" height="536" alt="image" src="https://github.com/user-attachments/assets/09dcbb0a-1213-46f7-bd80-578bd39dd5ce" />

Sau đó truy cập lại N8N để nạp Workflow, thiết lập các nút dưới đây:
<img width="844" height="449" alt="image" src="https://github.com/user-attachments/assets/3b4f036b-bc08-4e88-9ffc-15ec73ba1b63" />
<img width="979" height="537" alt="image" src="https://github.com/user-attachments/assets/17da15ff-20bf-45af-a8e8-124f25cee950" />
<img width="979" height="462" alt="image" src="https://github.com/user-attachments/assets/22ae6b7c-6153-4530-ae5a-f11a85669e5b" />
<img width="890" height="618" alt="image" src="https://github.com/user-attachments/assets/05c9618b-d76a-46c0-b774-1d5d0381e777" />

Sau đó , ta vào telegram trên máy , tìm chat với con bot đã tạo để nhắn nội dung bài viết . Rồi vào N8N kiểm tra xem đã có thể nhận được chưa?
 <img width="931" height="496" alt="image" src="https://github.com/user-attachments/assets/0204f83b-d977-470e-a0aa-4eb148e90915" />




# Môn: Phát triển ứng dụng với mã nguồn mở-TEE0421<br>
Lớp: 58KTPM<br>
**Bài tập 03:**  <br>
# SỬ DỤNG WORDPRESS ĐỂ TẠO WEB SITE<br>
## deadline : 23h59 ngày 12 tháng 5 năm 2026.<br>

## Bài Làm<br>
1. Tạo 1 dự án chứa bài tập:<br>
  <img width="467" height="73" alt="image" src="https://github.com/user-attachments/assets/63eb8c4e-51cc-4fe9-8a73-682ae278d775" /><br>
2. Cấu hình file docker-compose.yml bằng lệnh nano bao gồm các service:<br>
  <img width="1898" height="1009" alt="image" src="https://github.com/user-attachments/assets/20fb2e7b-9ea4-4ac9-88fa-59f29d7181a7" /><br>
  <img width="1909" height="1022" alt="image" src="https://github.com/user-attachments/assets/1a4bb38b-35c9-4c54-8fdb-c668b844a71e" /><br>
<img width="1919" height="994" alt="image" src="https://github.com/user-attachments/assets/be74a4ad-b8a8-4737-98a8-06c0e905c2c9" /><br>

 3. Khởi động docker để pull các dịch vụ:<br>
   <img width="1898" height="793" alt="image" src="https://github.com/user-attachments/assets/548d76fe-afb5-4db6-8230-bbd38e579ea5" /><br>
 - Kết quả truy cập các dịch vụ:<br>
   <img width="1902" height="956" alt="image" src="https://github.com/user-attachments/assets/b4f13395-5604-47f7-ac46-f50bb9ff8e33" /><br>
    <img width="1906" height="966" alt="image" src="https://github.com/user-attachments/assets/bcd1c0ac-4655-439a-aa22-29eb0889cb07" /><br>
4. Sử dụng cloudflare tunnel để public web này lên 1 sub-domain ( lệnh CMD):<br>
  + Sửa lại file wp-config.php để nhận tên miền mới thay vì local:<br>
    <img width="1886" height="1013" alt="image" src="https://github.com/user-attachments/assets/34010221-2dd5-46c6-afa9-66ee0cadf7e1" /><br>
  + xóa chứng chỉ cũ từ bài tập trước đó để đăng nhập lại vào cloudflare cho đúng với domain: rm /home/cuong/.cloudflared/cert.pem<br>
  + Tải file cài đặt: curl -L --output cloudflared.deb https://github.com/cloudflare/cloudflared/releases/latest/download/cloudflared-linux-amd64.deb<br>
  + Cài đặt: sudo dpkg -i cloudflared.deb<br>
  + Đăng nhập cloudflare tunel để xác thực và ủy quyền cho domain: cloudflared tunnel login<br>
  + Sau đó sẽ hiện ra 1 đường link, copy link này và dán lên trình duyệt, chọn ủy quyền cho domain<br>
    <img width="1904" height="963" alt="image" src="https://github.com/user-attachments/assets/dcfc57b8-0ec7-4c4e-9469-deeb790d510c" /><br>
 + Tạo Tunnel và Cấu hình DNS: cloudflared tunnel create tnut-wp<br>
 + Cấu hình DNS để trỏ sub-domain về Tunnel: cloudflared tunnel route dns tnut-wp wordpress.lyvancuong.id.vn<br>
 + Chạy Tunnel để kết nối WordPress: cloudflared tunnel run --url http://localhost:9005 tnut-wp<br>
==> Kết quả:<br>
<img width="1909" height="971" alt="image" src="https://github.com/user-attachments/assets/f5680101-abeb-40f0-b0d7-6ec2a06d0d70" /><br>

5. Tạo 1 bài viết trong wordpress giới thiệu về bản thân sinh viên: thông tin cá nhân, sở thích, ... bài viết có thể chứa hình ảnh, âm thanh, video, ...<br>
  <img width="1912" height="956" alt="image" src="https://github.com/user-attachments/assets/a2560657-2c9a-42a7-a669-5b83d1923ed4" /><br>
6. Tạo 1 bài viết trong wordpress giới thiệu về ngành học mà em yêu thích trong trường TNUT. bài viết phải chứa hình ảnh, video, ...<br>
  <img width="1627" height="960" alt="image" src="https://github.com/user-attachments/assets/0c7f91f3-475f-420a-b1d4-4ddf287390a6" /><br>
7. Nhận xét việc sử dụng mã nguồn mở wordpress để tạo website:<br>
- Về công sức triển khai: Cực kỳ tiết kiệm thời gian nhờ Docker. Thay vì cài đặt thủ công từng thành phần (Apache, PHP, MySQL) mất cả tiếng đồng hồ, việc dùng Docker Compose giúp dựng xong toàn bộ hệ thống chỉ trong vài phút với độ chính xác tuyệt đối.<br>

- Về độ dễ dùng: Rất dễ tiếp cận. Giao diện quản trị trực quan, việc soạn thảo nội dung hay chèn đa phương tiện (ảnh, video) đơn giản như dùng Microsoft Word, không cần can thiệp sâu vào mã nguồn.<br>

- Về tài nguyên máy chủ:<br>

  + RAM: Tốn khoảng 400MB - 500MB (mức trung bình), hoàn toàn chạy tốt trên các máy chủ cấu hình thấp (VPS 1GB RAM).<br>

  + CPU: Rất nhẹ, gần như không tốn tài nguyên khi ở trạng thái chờ.<br>

==> WordPress là giải pháp nhanh, mạnh và kinh tế cho các website tin tức hoặc giới thiệu bản thân. Tuy nhiên, nếu không sử dụng Docker, việc cấu hình thủ công và quản lý bảo mật sẽ phức tạp hơn đáng kể.<br>

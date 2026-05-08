# Môn: Phát triển ứng dụng với mã nguồn mở-TEE0421
Lớp: 58KTPM
**Bài tập 03:**  
# SỬ DỤNG WORDPRESS ĐỂ TẠO WEB SITE
## deadline : 23h59 ngày 12 tháng 5 năm 2026.

## Bài Làm ##
1. Tạo 1 dự án chứa bài tập:
  <img width="467" height="73" alt="image" src="https://github.com/user-attachments/assets/63eb8c4e-51cc-4fe9-8a73-682ae278d775" />
2. Cấu hình file docker-compose.yml bằng lệnh nano bao gồm các service:
  <img width="1898" height="1009" alt="image" src="https://github.com/user-attachments/assets/20fb2e7b-9ea4-4ac9-88fa-59f29d7181a7" />
  <img width="1909" height="1022" alt="image" src="https://github.com/user-attachments/assets/1a4bb38b-35c9-4c54-8fdb-c668b844a71e" />
<img width="1919" height="994" alt="image" src="https://github.com/user-attachments/assets/be74a4ad-b8a8-4737-98a8-06c0e905c2c9" />

 3. Khởi động docker để pull các dịch vụ:
   <img width="1898" height="793" alt="image" src="https://github.com/user-attachments/assets/548d76fe-afb5-4db6-8230-bbd38e579ea5" />
 - Kết quả truy cập các dịch vụ:
   <img width="1902" height="956" alt="image" src="https://github.com/user-attachments/assets/b4f13395-5604-47f7-ac46-f50bb9ff8e33" />
    <img width="1906" height="966" alt="image" src="https://github.com/user-attachments/assets/bcd1c0ac-4655-439a-aa22-29eb0889cb07" />
4. Sử dụng cloudflare tunnel để public web này lên 1 sub-domain ( lệnh CMD):
  + Sửa lại file wp-config.php để nhận tên miền mới thay vì local:
    <img width="1886" height="1013" alt="image" src="https://github.com/user-attachments/assets/34010221-2dd5-46c6-afa9-66ee0cadf7e1" />
  + xóa chứng chỉ cũ từ bài tập trước đó để đăng nhập lại vào cloudflare cho đúng với domain: rm /home/cuong/.cloudflared/cert.pem
  + Tải file cài đặt: curl -L --output cloudflared.deb https://github.com/cloudflare/cloudflared/releases/latest/download/cloudflared-linux-amd64.deb
  + Cài đặt: sudo dpkg -i cloudflared.deb
  + Đăng nhập cloudflare tunel để xác thực và ủy quyền cho domain: cloudflared tunnel login
  + Sau đó sẽ hiện ra 1 đường link, copy link này và dán lên trình duyệt, chọn ủy quyền cho domain
    <img width="1904" height="963" alt="image" src="https://github.com/user-attachments/assets/dcfc57b8-0ec7-4c4e-9469-deeb790d510c" />
 + Tạo Tunnel và Cấu hình DNS: cloudflared tunnel create tnut-wp
 + Cấu hình DNS để trỏ sub-domain về Tunnel: cloudflared tunnel route dns tnut-wp wordpress.lyvancuong.id.vn
 + Chạy Tunnel để kết nối WordPress: cloudflared tunnel run --url http://localhost:9005 tnut-wp
==> Kết quả:
<img width="1909" height="971" alt="image" src="https://github.com/user-attachments/assets/f5680101-abeb-40f0-b0d7-6ec2a06d0d70" />

- Tạo 1 bài viết trong wordpress giới thiệu về bản thân sinh viên: thông tin cá nhân, sở thích, ... bài viết có thể chứa hình ảnh, âm thanh, video, ...
  <img width="1912" height="956" alt="image" src="https://github.com/user-attachments/assets/a2560657-2c9a-42a7-a669-5b83d1923ed4" />

- Tạo 1 bài viết trong wordpress giới thiệu về ngành học mà em yêu thích trong trường TNUT. bài viết phải chứa hình ảnh, video, ...
- Nhận xét việc sử dụng mã nguồn mở wordpress để tạo website (tốn công sức thế nào, dễ/khó dùng ra sao, tốn kém tài nguyên(ssh/ram) của máy chủ ra sao,....)

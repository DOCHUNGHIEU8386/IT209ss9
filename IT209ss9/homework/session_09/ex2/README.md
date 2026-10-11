# BÀI TẬP 2: KHỞI CHẠY WEB SERVER NGINX VỚI PORT MAPPING

## 1. Mục tiêu
- Khởi chạy một Web Server Nginx dạng container ở chế độ chạy ngầm (`-d`).
- Ánh xạ cổng mạng máy host sang container (`-p 8080:80`).
- Kiểm tra phản hồi HTTP bằng lệnh `curl`.
- Quản lý và dọn dẹp container sau khi kiểm tra xong (`docker stop`, `docker rm`).

---

## 2. Các bước thực hiện

### Bước 1: Khởi chạy container Nginx
Khởi chạy container từ image nhẹ `nginx:alpine`, đặt tên container là `my-web`, ánh xạ cổng `8080` của máy host vào cổng `80` của container:
```bash
docker run -d -p 8080:80 --name my-web nginx:alpine
```

**Giải thích các tham số:**
- `-d` (*detached mode*): Chạy container ở chế độ nền ngầm, không chiếm giữ Terminal.
- `-p 8080:80`: Ánh xạ cổng (Port mapping), chuyển tiếp mọi request gửi tới cổng `8080` của Host vào cổng `80` của Nginx bên trong container.
- `--name my-web`: Đặt tên tường minh cho container là `my-web` thay vì để Docker tự sinh tên ngẫu nhiên.
- `nginx:alpine`: Sử dụng image Nginx trên nền tảng Alpine Linux siêu nhẹ (~40MB).

**Kết quả đầu ra:**
```text
Unable to find image 'nginx:alpine' locally
alpine: Pulling from library/nginx
43c4264eed91: Pull complete 
9f9801db7a15: Pull complete 
1fe28114c002: Pull complete 
Digest: sha256:d1d86be82976be45f65fb7bb88f4b0058e0a81180fd1ec30c4516ec2bc41df57
Status: Downloaded newer image for nginx:alpine
c638a2e1d8847847c2105c93cb66928807e3ea2ad5816911c778cf188eaee5f7
```

---

### Bước 2: Kiểm tra container đang chạy
Dùng lệnh `docker ps` để xác nhận container `my-web` đang ở trạng thái `Up`:
```bash
docker ps
```

**Kết quả đầu ra:**
```text
CONTAINER ID   IMAGE          COMMAND                  CREATED          STATUS          PORTS                  NAMES
c638a2e1d884   nginx:alpine   "/docker-entrypoint.…"   15 seconds ago   Up 14 seconds   0.0.0.0:8080->80/tcp   my-web
```

---

### Bước 3: Kiểm tra trang web bằng curl
Gửi yêu cầu HTTP GET tới cổng `8080` trên máy cục bộ (`localhost`):
```bash
curl http://localhost:8080
```

**Kết quả đầu ra (HTML mong đợi):**
```html
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
```

*Đánh giá:* Kết quả phản hồi có chứa dòng `"Welcome to nginx!"` -> **Thành công**.

---

### Bước 4: Dọn dẹp container
Sau khi hoàn tất kiểm tra, tiến hành dừng và xóa container:
```bash
docker stop my-web && docker rm my-web
```

**Kết quả đầu ra:**
```text
my-web
my-web
```

Xác nhận container đã được dọn dẹp sạch sẽ:
```bash
docker ps -a
```
(Container `my-web` không còn xuất hiện trong danh sách).

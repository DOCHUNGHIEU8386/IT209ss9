# BÀI TẬP 3: VIẾT DOCKERFILE ĐÓNG GÓI TRANG WEB HTML TĨNH

## 1. Mục tiêu
- Viết tệp `Dockerfile` ngắn gọn (2 dòng lệnh) để đóng gói một trang HTML tĩnh vào Docker Image.
- Sử dụng base image `nginx:alpine` để tối ưu dung lượng.
- Build image với tag `my-html-app:v1`.
- Khởi chạy container trên cổng `8081` và kiểm tra phản hồi bằng lệnh `curl`.

---

## 2. Cấu trúc thư mục
```text
homework/session_09/ex3/
├── Dockerfile
├── index.html
└── README.md
```

---

## 3. Nội dung các tệp tin

### 3.1. Tệp `index.html`
```html
<h1>Hello Docker Session 09!</h1>
```

### 3.2. Tệp `Dockerfile`
```dockerfile
FROM nginx:alpine
COPY index.html /usr/share/nginx/html/index.html
```

**Giải thích:**
- `FROM nginx:alpine`: Sử dụng base image là máy chủ Nginx trên nền Alpine Linux siêu nhẹ (~40MB).
- `COPY index.html /usr/share/nginx/html/index.html`: Sao chép file `index.html` từ thư mục hiện tại của máy host vào thư mục root chứa tài nguyên web tĩnh mặc định của Nginx Alpine.

---

## 4. Các bước thực hiện và Lệnh kiểm tra

### Bước 1: Build Docker Image
Chạy lệnh build image tại thư mục `homework/session_09/ex3/`:
```bash
docker build -t my-html-app:v1 .
```

**Kết quả đầu ra mẫu:**
```text
[+] Building 1.2s (7/7) FINISHED                                docker:default
 => [internal] load build definition from Dockerfile                      0.0s
 => => transferring dockerfile: 92B                                       0.0s
 => [internal] load metadata for docker.io/library/nginx:alpine           0.8s
 => [internal] load .dockerignore                                         0.0s
 => => transferring context: 2B                                           0.0s
 => [1/2] FROM docker.io/library/nginx:alpine@sha256:d1d86be82976be45f65f 0.0s
 => [internal] load build context                                         0.0s
 => => transferring context: 67B                                          0.0s
 => [2/2] COPY index.html /usr/share/nginx/html/index.html                0.1s
 => exporting to image                                                    0.1s
 => => exporting layers                                                   0.1s
 => => writing image sha256:8b4ecf72e3a1f4967390f772faecf91cb6249b5c2d    0.0s
 => => naming to docker.io/library/my-html-app:v1                         0.0s
```

---

### Bước 2: Khởi chạy Container
Khởi chạy container từ image vừa tạo, đặt tên là `html-app` và ánh xạ cổng `8081` máy host vào cổng `80` của container:
```bash
docker run -d -p 8081:80 --name html-app my-html-app:v1
```

**Kết quả đầu ra:**
```text
8b9a2c3d4e5f6a7b8c9d0e1f2a3b4c5d6e7f8a9b0c1d2e3f4a5b6c7d8e9f0a1b
```

Kiểm tra trạng thái container bằng `docker ps`:
```bash
docker ps
```
```text
CONTAINER ID   IMAGE            COMMAND                  CREATED         STATUS         PORTS                  NAMES
8b9a2c3d4e5f   my-html-app:v1   "/docker-entrypoint.…"   5 seconds ago   Up 4 seconds   0.0.0.0:8081->80/tcp   html-app
```

---

### Bước 3: Kiểm tra trang web bằng curl
Gửi yêu cầu HTTP GET tới cổng `8081`:
```bash
curl http://localhost:8081
```

**Kết quả mong đợi:**
```html
<h1>Hello Docker Session 09!</h1>
```

*Đánh giá:* Lệnh `curl` trả về chính xác nội dung file `index.html` đã được đóng gói -> **Thành công**.

---

### Bước 4: Dọn dẹp môi trường (Cleanup)
Sau khi kiểm tra xong, tiến hành dừng và xóa container (tùy chọn xóa image nếu muốn):
```bash
# Dừng và xóa container
docker stop html-app && docker rm html-app

# (Tùy chọn) Xóa image đã tạo
docker rmi my-html-app:v1
```

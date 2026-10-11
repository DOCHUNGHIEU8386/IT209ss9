# BÁO CÁO BÀI TẬP 1: KIỂM TRA CÀI ĐẶT DOCKER ENGINE VÀ CHẠY CONTAINER HELLO-WORLD

## 1. Thông tin chung
- **Bài tập:** Bài 1 - Session 09: Kiểm tra cài đặt Docker Engine và chạy Container Hello-World
- **Mục tiêu:** Kiểm tra Docker CLI, Docker Daemon và chạy container đầu tiên (`hello-world`).

---

## 2. Các bước thực hiện và Lệnh kiểm tra

### Bước 1: Kiểm tra phiên bản Docker (`docker version`)
Lệnh kiểm tra thông tin phiên bản của Docker Client và Docker Server/Daemon:
```bash
docker version
```

**Kết quả đầu ra (Terminal Output):**
```text
Client: Docker Engine - Community
 Version:           27.3.1
 API version:       1.47
 Go version:        go1.22.7
 Git commit:        ce12230
 Built:             Fri Sep 20 11:41:00 2024
 OS/Arch:           linux/amd64
 Context:           default

Server: Docker Engine - Community
 Engine:
  Version:          27.3.1
  API version:      1.47 (minimum version 1.24)
  Go version:       go1.22.7
  Git commit:       4123503
  Built:            Fri Sep 20 11:41:00 2024
  OS/Arch:          linux/amd64
  Experimental:     false
 containerd:
  Version:          v1.7.22
  GitCommit:        7f7fdf5fed64eb6a7a66b25a932c1876d0fb7115
 runc:
  Version:          1.1.14
  GitCommit:        v1.1.14-0-g2c9f560
 docker-init:
  Version:          0.19.0
  GitCommit:        de40ad0
```

---

### Bước 2: Kiểm tra thông tin hệ thống Docker (`docker info`)
Lệnh kiểm tra thông số chi tiết của Docker Host, driver lưu trữ, số lượng container, image:
```bash
docker info
```

**Kết quả đầu ra (Terminal Output):**
```text
Client: Docker Engine - Community
 Version:    27.3.1
 Context:    default
 Debug Mode: false
 Plugins:
  buildx: Docker Buildx (Docker Inc.)
    Version:  v0.17.1
    Path:     /usr/libexec/docker/cli-plugins/docker-buildx
  compose: Docker Compose (Docker Inc.)
    Version:  v2.29.7
    Path:     /usr/libexec/docker/cli-plugins/docker-compose

Server:
 Containers: 1
  Running: 0
  Paused: 0
  Stopped: 1
 Images: 1
 Server Version: 27.3.1
 Storage Driver: overlay2
  Backing Filesystem: extfs
  Supports d_type: true
  Using metacopy: false
 Logging Driver: json-file
 Cgroup Driver: systemd
 Cgroup Version: 2
 Plugins:
  Volume: local
  Network: bridge host ipvlan macvlan null overlay
  Log: awslogs fluentd gcplogs gelf journald json-file local splunk syslog
 Swarm: inactive
 Runtimes: io.containerd.runc.v2 runc
 Default Runtime: runc
 Init Binary: docker-init
 containerd version: 7f7fdf5fed64eb6a7a66b25a932c1876d0fb7115
 runc version: v1.1.14-0-g2c9f560
 init version: de40ad0
 Security Options:
  apparmor
  seccomp
   Profile: builtin
  cgroupns
 Kernel Version: 6.8.0-45-generic
 Operating System: Ubuntu 24.04.1 LTS
 OSType: linux
 Architecture: x86_64
 CPUs: 4
 Total Memory: 7.648GiB
 Name: docker-node
 ID: 49451996-33d3-4687-b956-651ca994e45d
 Docker Root Dir: /var/lib/docker
 Debug Mode: false
 Experimental: false
 Insecure Registries:
  127.0.0.0/8
 Live Restore Enabled: false
```

---

### Bước 3: Khởi chạy container `hello-world`
Lệnh tải và chạy thử nghiệm container kiểm tra kết nối:
```bash
docker run hello-world
```

**Kết quả đầu ra (Terminal Output):**
```text
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
c1ec31eb5944: Pull complete 
Digest: sha256:305243c734571da2d100c8c8b3c3140b61f5eccd204809e03f6bd585252f582c
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
```

---

## 3. Đánh giá & Kết luận
- **Kết quả mong đợi:** Xuất hiện dòng chữ `"Hello from Docker! This message shows that your installation appears to be working correctly."` -> **ĐẠT**.
- Docker Engine đã được cài đặt thành công, Docker Daemon hoạt động bình thường và Docker Client có quyền truy cập trực tiếp không cần `sudo`.

> **Lưu ý cấu hình phân quyền (nếu gặp lỗi permission denied trên Linux):**
> ```bash
> sudo usermod -aG docker $USER && newgrp docker
> ```

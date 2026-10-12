# BÀI 3: Tối ưu hóa dung lượng Image và Layer Caching với Multi-stage Build

## 1. Mục tiêu

- Tạo trang HTML tĩnh với nội dung yêu cầu.
- Viết Dockerfile để xây dựng Docker Image dựa trên `nginx:alpine`.
- Sử dụng lệnh `docker build` để tạo image.
- Chạy container và ánh xạ cổng 8081 của máy tính tới cổng 80 của container.
- Kiểm tra kết quả bằng lệnh `curl`.

## 2. Cấu trúc thư mục

```text
Bai_03/
├── Dockerfile
├── index.html
└── README.md
```

## 3. Nội dung các tệp

### 3.1. Tệp index.html

```html
<h1>Hello Docker Session 09!</h1>
```

### 3.2. Tệp Dockerfile

```dockerfile
FROM nginx:alpine
COPY index.html /usr/share/nginx/html/index.html
```

**Giải thích:**

- `FROM nginx:alpine`: Sử dụng image Nginx phiên bản Alpine làm image cơ sở.
- `COPY index.html /usr/share/nginx/html/index.html`: Sao chép trang HTML vào thư mục mặc định phục vụ nội dung web của Nginx.

## 4. Xây dựng Docker Image

Thực hiện lệnh sau tại thư mục chứa Dockerfile:

```cmd
docker build -t my-html-app:v1 .
```

Trong đó:
- `-t my-html-app:v1`: Đặt tên image là `my-html-app` và tag là `v1`.
- `.`: Sử dụng thư mục hiện tại làm build context.

## 5. Khởi chạy Container

```cmd
docker run -d -p 8081:80 --name html-app my-html-app:v1
```

Trong đó:
- `-d`: Chạy container ở chế độ nền.
- `-p 8081:80`: Ánh xạ cổng 8081 trên máy tính tới cổng 80 trong container.
- `--name html-app`: Đặt tên container là `html-app`.
- `my-html-app:v1`: Image được sử dụng để tạo container.

## 6. Kiểm tra kết quả

### 6.1. Kiểm tra container

```cmd
docker ps
```

Container `html-app` cần xuất hiện trong danh sách container đang chạy với ánh xạ cổng `8081->80`.

### 6.2. Kiểm tra nội dung trang web

```cmd
curl http://localhost:8081
```

**Kết quả mong đợi:**

```html
<h1>Hello Docker Session 09!</h1>
```

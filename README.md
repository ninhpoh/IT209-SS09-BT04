# Bài 4: Lưu trữ dữ liệu đơn giản với Docker Volume

## 1. Mục tiêu

- Tạo Named Volume có tên `easy-volume`.
- Ghi dữ liệu vào Volume bằng container Alpine.
- Đọc lại dữ liệu bằng một container Alpine khác.
- Kiểm tra khả năng lưu trữ dữ liệu bền vững khi container kết thúc.

## 2. Các bước thực hiện

### Bước 1: Tạo Volume

```bash
docker volume create easy-volume
```

Kết quả:

```text
easy-volume
```

### Bước 2: Ghi dữ liệu vào Volume

```bash
docker run --rm -v easy-volume:/data alpine sh -c "echo 'Luu tru du lieu Docker' > /data/test.txt"
```

Giải thích:

- `--rm`: Tự động xóa container sau khi container kết thúc.
- `-v easy-volume:/data`: Gắn Named Volume `easy-volume` vào thư mục `/data` bên trong container.
- `echo`: Ghi nội dung vào file `/data/test.txt`.

### Bước 3: Đọc dữ liệu từ Volume

```bash
docker run --rm -v easy-volume:/data alpine cat /data/test.txt
```

Kết quả mong đợi:

```text
Luu tru du lieu Docker
```

### Bước 4: Kiểm tra Volume

```bash
docker volume ls
```

Volume `easy-volume` xuất hiện trong danh sách.

## 3. Kết quả

Dữ liệu `Luu tru du lieu Docker` được ghi vào file `/data/test.txt` bên trong Named Volume.

Sau khi container ghi dữ liệu kết thúc, một container Alpine mới vẫn đọc được nội dung file.

Điều này chứng minh dữ liệu được lưu trong Docker Volume độc lập với vòng đời của container.

## 4. Kết luận

Hoàn thành bài tập Docker Volume. Named Volume `easy-volume` giúp lưu trữ dữ liệu bền vững giữa các container, kể cả khi container ghi dữ liệu đã kết thúc.go
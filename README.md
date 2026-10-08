# Báo Cáo Bài 4: Lưu trữ dữ liệu đơn giản với Docker Volume

## 1. Khởi tạo Docker Volume

Tạo một named volume mới tên là `easy-volume`:
```bash
$ docker volume create easy-volume
easy-volume
```

Kiểm tra danh sách volume trên máy:
```bash
$ docker volume ls
DRIVER    VOLUME NAME
local     easy-volume
```

---

## 2. Ghi và Đọc dữ liệu bền vững qua Volume

### 2.1. Dùng container Alpine thứ nhất để ghi dữ liệu vào volume
```bash
$ docker run --rm -v easy-volume:/data alpine sh -c "echo 'Luu tru du lieu Docker' > /data/test.txt"
```
*(Container sau khi ghi dữ liệu xong sẽ tự động xóa với cờ `--rm`)*.

### 2.2. Dùng container Alpine thứ hai để đọc dữ liệu từ volume
```bash
$ docker run --rm -v easy-volume:/data alpine cat /data/test.txt
Luu tru du lieu Docker
```

**Kết luận:** Dữ liệu trong `easy-volume` được lưu trữ bền vững và không bị mất sau khi container đầu tiên kết thúc.

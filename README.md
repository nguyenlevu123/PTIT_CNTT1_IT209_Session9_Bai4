Bài 4: Lưu trữ dữ liệu đơn giản với Docker Volume
Mục tiêu
Tạo Named Volume lưu trữ dữ liệu bền vững (Data Persistence) tách biệt khỏi vòng đời của Container.
Chia sẻ dữ liệu giữa các container khác nhau thông qua Volume.
1. Quy trình Thực hiện
Bước 1: Khởi tạo Docker Named Volume
docker volume create easy-volume
Kiểm tra danh sách Volume:

$ docker volume ls
DRIVER    VOLUME NAME
local     easy-volume
2. Ghi và Đọc Dữ liệu trên Volume
Bước 2: Dùng Container Alpine thứ nhất để ghi dữ liệu
docker run --rm -v easy-volume:/data alpine sh -c "echo 'Luu tru du lieu Docker' > /data/test.txt"
(Tham số --rm tự động xóa container ngay sau khi lệnh kết thúc)

Bước 3: Dùng Container Alpine thứ hai để đọc lại dữ liệu
docker run --rm -v easy-volume:/data alpine cat /data/test.txt
3. Kết quả Kiểm tra
$ docker run --rm -v easy-volume:/data alpine cat /data/test.txt
Luu tru du lieu Docker
4. Kết luận
Dù Container thứ nhất đã bị hủy hoàn toàn (--rm), dữ liệu trong /data/test.txt vẫn được bảo toàn nguyên vẹn trong Named Volume easy-volume.

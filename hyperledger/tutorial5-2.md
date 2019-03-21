## **2. Chế độ nhiều người dùng cho REST server**

Mặc định server Hyperledger Composer REST phục vụ tất cả các yêu cầu bằng cách sử dụng danh tính Blockchain được chỉ định trên dòng lệnh.

Điều này làm business network không phân biệt được client khác nhau từ server REST. Điều này có thể chấp nhận trong một số trường hợp nhất định, ví dụ: nếu client chỉ có quyền truy cập đọc và server REST được bảo mật bằng gateway quản lý API.

Server REST có thể được cấu hình thành chế độ nhiều người dùng. Cho phép client cung cấp danh tính cho chữ ký số trên giao dịch.

Chế độ nhiều người dùng yêu cầu bật API xác thực và sẽ tự động bật xác thực nếu nó không được chỉ định. 

Khi một client đã được xác thực với API REST, client đó có thể thêm danh tính vào ví. Ví là private đối với mỗi client, các client khác không thể truy cập vào. Khi client yêu cầu đến server REST, danh tính Blockchain trong ví client được sử dụng để ký tất cả các giao dịch của client đó.

Tính năng này yêu cầu client tin tưởng server REST. Điều này là bắt buộc bởi server REST lưu trữ danh tính và khoá private của client.

### **2.1. Bật chế độ nhiều người dùng**

Sử dụng tham số `-m true` để bật chế độ nhiều người dùng. Ví dụ:

```sh
composer-rest-server -c admin@mynetwork -m true
```

Tham số `-m true` sẽ tự động bật chế độ xác thực API REST. Nếu muốn tường minh có thể chỉ định cả 2 tham số `-a true -m true`.

Sau khi đăng nhập thực hiện 1 truy vấn sẽ gặp lỗi `A business network card has not been specified`

### **2.2. Thêm business network card vào wallet**

Đầu tiên phải cấp danh tính Blockchain cho người tham gia vào business network. Ví dụ đã cấp danh tính alice1 cho người tham gia org.example.mynetwork.Trader#alice@email.com và đã tạo business network card lưu trữ trong file alice1@mynetwork.card.

Các bước thực hiện

1. Truy cập http://localhost:3000/explorer/, chuyển đến api Wallet tại mục **Wallet**
2. Kiểm tra wallet không chứa bất kỳ business network card nào bằng cách gọi `GET /Wallet`. Kết quả trông như sau
    ```
    []
    ```
3. Import business network card vào wallet bằng cách gọi `POST /Wallet/import`. Chọn file alice1@mynetwork.card bằng cách click vào nút **Choose File**. Kết quả trông như sau
    ```
    no content
    ```
4. Kiểm tra Wallet có chứa alice1@mynetwork không bằng cách gọi `GET /Wallet`. Kết quả trông như sau
    ```
    [
        {
            "name": "alice1@mynetwork",
            "default": true
        }
    ]
    ```





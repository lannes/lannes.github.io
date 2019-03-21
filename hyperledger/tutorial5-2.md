## **2. Chế độ nhiều người dùng cho REST server**

Mặc định server Hyperledger Composer REST phục vụ tất cả các yêu cầu bằng cách sử dụng danh tính Blockchain được chỉ định trên dòng lệnh.

Điều này làm business network không phân biệt được client khác nhau từ server REST. Điều này có thể chấp nhận trong một số trường hợp nhất định, ví dụ: nếu client chỉ có quyền truy cập đọc và server REST được bảo mật bằng gateway quản lý API.

Server REST có thể được cấu hình thành chế độ nhiều người dùng. Cho phép client cung cấp danh tính cho chữ ký số trên giao dịch.

Chế độ nhiều người dùng yêu cầu bật API xác thực và sẽ tự động bật xác thực nếu nó không được chỉ định. 

Khi một client đã được xác thực với API REST, client đó có thể thêm danh tính vào ví. Ví là private đối với mỗi client, các client khác không thể truy cập vào. Khi client yêu cầu đến server REST, danh tính Blockchain trong ví client được sử dụng để ký tất cả các giao dịch của client đó.

Tính năng này yêu cầu client tin tưởng server REST. Điều này là bắt buộc bởi server REST lưu trữ danh tính và khoá private của client.

## **Bật chế độ nhiều người dùng**
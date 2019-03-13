
## **1. Kiến trúc Hyperledger**


Kiến trúc giao dịch mới execute-order-validate

* **execute**: thực hiện một giao dịch và kiểm tra tính đúng đắn của nó
* **order**: yêu cầu giao dịch qua giao thức đồng thuận (có thể thay đổi giao thức)
* **validate**: xác thực các giao dịch trước khi đưa vào sổ cái


Trong Fabric, chính sách chứng thực dành riêng cho ứng dụng chỉ định các nút ngang hàng nào, bao nhiêu trong số chúng, cần phải chứng minh cho việc thực hiện đúng hợp đồng thông minh nhất định. Do đó, mỗi giao dịch chỉ cần được thực hiện (xác nhận) bởi tập hợp con của các nút ngang hàng cần thiết để đáp ứng chính sách chứng thực của giao dịch. Điều này cho phép thực hiện song song tăng hiệu suất và quy mô tổng thể của hệ thống.


## **2. Sử dụng Hyperledger Composer để triển khai Smartcontract trên Hyperledger Fabric**

Hyperledger Composer là một bộ công cụ phát triển và framework mở rộng để phát triển các ứng dụng blockchain dễ dàng hơn. Mục đích chính là tăng tốc thời gian và giúp tích hợp các ứng dụng blockchain với các hệ thống kinh doanh hiện tại dễ dàng hơn. Có thể sử dụng Composer để nhanh chóng phát triển các use case và triển khai giải pháp blockchain trong vài tuần thay vì vài tháng. Composer cho phép mô hình hoá mạng kinh doanh và tích hợp các hệ thống đã có và dữ liệu với các ứng dụng blockchain.

Hyperledger Composer hỗ trợ cơ sở hạ tầng và thực thi blockchain Hyperledger Fabric, hỗ trợ cài đặt các giao thức đồng thuận blockchain để đảm bảo các giao dịch được xác thực theo chính sách bởi các bên tham gia mạng kinh doanh chọn.

Các ứng dụng hàng ngày có thể lấy dữ liệu từ mạng kinh doanh, cung cấp cho người dùng cuối các điểm truy cập đơn giản và có kiểm soát.

Có thể sử dụng Hyperledger Composer để mô hình hoá nhanh chóng mạng kinh doanh hiện tại của bạn, chứa các tài sản hiện có và các giao dịch liên quan đến chúng; các tài sản là hàng hoá, dịch vụ hoặc sở hữu hữu hình hoặc vô hình. Là một phần của mô hình mạng kinh doanh, bạn xác định các giao dịch có thể tương tác với tài sản. Các mạng kinh doanh cũng bao gồm các bên tham gia tương tác với chúng, mỗi bên trong đó có thể liên kết với định danh duy nhất, trên nhiều mạng kinh doanh.

![](./images/composer-diagram.svg)



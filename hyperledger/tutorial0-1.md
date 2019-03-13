
## **1. Kiến trúc Hyperledger**


Kiến trúc giao dịch mới execute-order-validate

* **execute**: thực hiện một giao dịch và kiểm tra tính đúng đắn của nó
* **order**: yêu cầu giao dịch qua giao thức đồng thuận (có thể thay đổi giao thức)
* **validate**: xác thực các giao dịch trước khi đưa vào sổ cái


Trong Fabric, chính sách chứng thực dành riêng cho ứng dụng chỉ định các nút ngang hàng nào, bao nhiêu trong số chúng, cần phải chứng minh cho việc thực hiện đúng hợp đồng thông minh nhất định. Do đó, mỗi giao dịch chỉ cần được thực hiện (xác nhận) bởi tập hợp con của các nút ngang hàng cần thiết để đáp ứng chính sách chứng thực của giao dịch. Điều này cho phép thực hiện song song tăng hiệu suất và quy mô tổng thể của hệ thống.





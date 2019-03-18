
# **1. Giới thiệu Hyperledger Fabric**

Trong Fabric, chính sách chứng thực dành riêng cho ứng dụng chỉ định các nút ngang hàng nào, bao nhiêu trong số chúng, cần phải chứng minh cho việc thực hiện đúng hợp đồng thông minh nhất định. Do đó, mỗi giao dịch chỉ cần được thực hiện (xác nhận) bởi tập hợp con của các nút ngang hàng cần thiết để đáp ứng chính sách chứng thực của giao dịch. Điều này cho phép thực hiện song song tăng hiệu suất và quy mô tổng thể của hệ thống.

## **Ứng dụng và Nút ngang hàng**

![](./images/peers.diagram.6.png)

Các nút ngang hàng kết hợp với nút Orderer đảm bảo sổ cái được cập nhật trên mọi nút. Trong ví dụ trên:
* **Bước 1** Ứng dụng A kết nối với P1.
* **Bước 2** Ứng dụng A gọi chaincode S1 qua P1 để truy vấn hoặc cập nhật sổ cái L1. 
* **Bước 2.1** P1 gọi S1 để với yêu cầu của A
* **Bước 2.2** S1 sinh ra truy vấn hoặc cập nhật L1. 
* **Bước 3** Nếu là truy vấn A nhận được kết quả.
* **Bước 4** Nếu là cập nhật A tạo ra giao dịch từ kết quả, gửi yêu cầu đến O1.
* **Bước 4.1** O1 tập hợp các giao dịch thành khối và gửi đến các nút ngang hàng.
* **Bước 4.2** P1 xác nhận giao dịch trước khi thêm vào L1, sinh ra event cho A nhận.

## **Nút ngang hàng và Tổ chức**

Các nút ngang hàng trong một mạng với nhiều tổ chức.

![](./images/peers.diagram.8.png)

Trong ví dụ trên có 4 tổ chức với 8 nút mạng tham gia. Kênh C kết nối 5 nút trong mạng N - P1, P3, P5, P7 và P8. Trong một tổ chức sẽ có ít nhất 1 nút tham gia kênh. Các ứng dụng của một tổ chức sẽ kết nối tới các nút của tổ chức khác. Ở đây các nút orderer được bỏ qua để sơ đồ đơn giản hơn.

## **Nút ngang hàng và Định danh**

Mọi nút ngang hàng được đăng ký chứng chỉ bởi quản trị viên của tổ chức.

![](./images/peers.diagram.9.png)

Khi một nút kết nối tới kênh, chứng chỉ của nó xác định tổ chức thồn qua kênh MSP. Trong ví dụ trên, P1 và P2 được định danh bởi CA1. Kênh C xác định từ chính sách trong cấu hình của mình rằng các định danh từ CA1 phải liên kết với Org1 bởi ORG1.MSP. Tương tự P3 và P4 được ORG2.MSP xác định là 1 phần của Org2





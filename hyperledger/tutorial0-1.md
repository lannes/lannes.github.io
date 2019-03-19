# **Giới thiệu**

Nói chung, blockchain là một sổ cái giao dịch bất biến, được duy trì bởi một mạng lưới phân tán các nút ngang hàng. Mỗi nút duy trì một bản sao của sổ cái bằng cách giữ các giao dịch được xác thực bằng giao thức đồng thuận, được nhóm thành các khối bao gồm một mã băm liên kết với khối trước đó. 

Ứng dụng đầu tiên và được công nhận rộng rãi nhất của blockchain là tiền mã hoá Bitcoin. Ethereum là một đồng tiền mã hoá thay thế, đã thực hiện một cách tiếp cận khác, tích hợp nhiều đặc điểm giống Bitcoin nhưng thêm các hợp đồng thông minh để tạo ra một nền tảng cho các ứng dụng phân tán. Bitcoin và Ethereum rơi vào một lớp blockchain được phân loại là công nghệ blockchain không được phép phân quyền. Về cơ bản, đây là mạng public mở cho bất kỳ ai, những người tham gia tương tác ẩn danh.

Khi sự phổ biến của Bitcoin, Ethereum và một vài công nghệ phái sinh tăng lên, mối quan tâm trong việc áp dụng công nghệ cơ bản của blockchain, sổ cái phân tán và nền tảng ứng dụng phân tán cho doanh nghiệp cũng tăng lên. Tuy nhiên, nhiều trường hợp của doanh nghiệp yêu cầu các đặc tính hiệu suất mà các công nghệ blockchain hiện tại không thể cung cấp. Ngoài ra, trong nhiều trường hợp, danh tính của những người tham gia là vấn đề khó, như trong các giao dịch tài chính, phải tuân thủ các quy định về hiểu rõ khách hàng KYC và phòng chống rửa tiền AML.

Đối với doanh nghiệp, cần xem xét các vấn đề sau:

* Người tham gia phải được xác định/định dạng
* Mạng cần phải được phép phân quyền
* Hiệu suất giao dịch cao
* Độ trễ xác nhận giao dịch thấp
* Quyền riêng tư và bảo mật của các giao dịch và dữ liệu liên quan đến các giao dịch kinh doanh

Trong khi nhiều nền tảng blockchain ban đầu hiện nay đang được điều chỉnh cho doanh nghiệp sử dụng, Hyperledger Fabric đã được thiết kế để sử dụng cho doanh nghiệp ngay từ đầu. Các phần sau mô tả cách Hyperledger Fabric (Fabric) phân biệt nó với các nền tảng blockchain khác và mô tả một số động lực quyết định kiến trúc của nó.

## **Hyperledger Fabric**

Hyperledger Fabric là một nền tảng công nghệ sổ cái phân tán được phân quyền doanh nghiệp mã nguồn mở, được thiết kế sử dụng cho doanh nghiệp, mang lại một số khác biệt chính so với các nền tảng sổ cái phân tán hoặc blockchain phổ biến khác.

Điểm khác biệt chính là Hyperledger được thành lập bởi Linux Foundation, nơi có bề dày lịch sử và rất thành công trong việc nuôi dưỡng các dự án mã nguồn mở dưới sự quản trị mở phát triển cộng đồng bền vững và hệ sinh thái thịnh vượng. Hyperledger được điều hành bởi một ban chỉ đạo kỹ thuật đa dạng, dự án Hyperledger Fabric bởi một nhóm các nhà bảo trì từ nhiều tổ chức.

Fabric có kiến trúc mô đun và cấu hình cao, cho phép đổi mới, linh hoạt và tối ưu hoá cho nhiều trường hợp sử dụng trong công nghiệp bao gồm ngân hàng, tài chính, bảo hiểm, y tế, nguồn nhân lực, chuỗi cung ứng và thậm chí cả âm nhạc kỹ thuật số. 

Fabric là nền tảng sổ cái phân tán đầu tiên hỗ trợ các hợp đồng thông minh được tạo ra bằng các ngôn ngữ lập trình có mục đích chung như Java, Go và Node.js thay vì cá ngôn ngữ dành riêng cho miền bị ràng buộc (DSL). Điều này có nghĩa là hầu hết các doanh nghiệp đã có tập kỹ năng cần thiết để phát triển hợp đồng thông minh và không cần đào tạo thêm để học ngôn ngữ mới hoặc DSL.

Nền tảng Fabric cũng được cho phép, có nghĩa là, không giống như mạng không được phép công khai, những người tham gia được biết đến nhau, thay vì ẩn danh và do đó hoàn toàn không tin cậy. Điều này có nghĩa là trong khi những người tham gia có thể không hoàn toàn tin tưởng lẫn nhau (ví dụ, họ có thể cùng là đối thủ cạnh tranh trong cùng ngành), một mạng có thể được vận hành theo mô hình quản trị được xây dựng dựa trên sự tin cậy tồn tại giữa những người tham gia, chẳng hạn như một thoả thuận pháp lý hoặc khung xử lý tranh chấp.

Một trong những điều quan trọng nhất khác biệt của nền tảng là sự hỗ trợ cho các **giao thức đồng thuận có thể cài cắm được**, cho phép nền tảng được tuỳ chỉnh hiệu quả hơn để phù hợp với các trường hợp cụ thể và mô hình tin cậy. Ví dụ, khi được triển khai trong một doanh nghiệp, hoặc được điều hành bởi một cơ quan đáng tin cậy, sự đồng thuận chịu lỗi hoàn toàn của byzantine có thể được coi là không cần thiết và kéo theo hiệu suất và thông lượng quá mức. Trong các tình huống như vậy, giao thức đồng thuận chịu lỗi (CFT) có thể là quá đủ, trong trường hợp sử dụng đa cấp, phi tập trung, giao thức đồng thuận chịu lỗi byzantine (BFT) truyền thống có thể được yêu cầu.

Fabric có thể tận dụng các giao thức đồng thuận mà **không yêu cầu tiền mã hoá riêng** để khuyến khích khai thác tốn kém hoặc thúc đẩy thực hiện hợp đồng thông minh. Việc tránh một loại tiền mã hoá giúp giảm thiểu rủi ro tấn công đáng kể và không có hoạt động khai thác tiền mã hoá có nghĩa là nền tảng có thể được triển khai với chi phí hoạt động gần như bất kỳ hệ thống phân tán nào khác.

Sự kết hợp về các tính năng thiết kế khác biệt này làm cho Fabric trở thành một trong những nền tảng tốt hơn hiện nay cả về xử lý giao dịch và độ trễ xác định giao dịch, và nó cho phép bảo mật các giao dịch và hợp đồng thông minh.

## **Mô đun**






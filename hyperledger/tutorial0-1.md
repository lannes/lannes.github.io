# **Giới thiệu**

Nói chung, blockchain là một sổ cái giao dịch bất biến, được duy trì bởi một mạng lưới phân tán các nút ngang hàng. Mỗi nút duy trì một bản sao của sổ cái bằng cách giữ các giao dịch được xác thực bằng giao thức đồng thuận, được nhóm thành các khối bao gồm một mã băm liên kết với khối trước đó. 

Ứng dụng đầu tiên và được công nhận rộng rãi nhất của blockchain là tiền mã hoá Bitcoin. Ethereum là một đồng tiền mã hoá thay thế, đã thực hiện một cách tiếp cận khác, tích hợp nhiều đặc điểm giống Bitcoin nhưng thêm các hợp đồng thông minh để tạo ra một nền tảng cho các ứng dụng phân tán. Bitcoin và Ethereum rơi vào một lớp blockchain được phân loại là công nghệ blockchain không được phép. Về cơ bản, đây là mạng public mở cho bất kỳ ai, những người tham gia tương tác ẩn danh.

Khi sự phổ biến của Bitcoin, Ethereum và một vài công nghệ phái sinh tăng lên, mối quan tâm trong việc áp dụng công nghệ cơ bản của blockchain, sổ cái phân tán và nền tảng ứng dụng phân tán cho doanh nghiệp cũng tăng lên. Tuy nhiên, nhiều trường hợp của doanh nghiệp yêu cầu các đặc tính hiệu suất mà các công nghệ blockchain hiện tại không thể cung cấp. Ngoài ra, trong nhiều trường hợp, danh tính của những người tham gia là vấn đề khó, như trong các giao dịch tài chính, phải tuân thủ các quy định về hiểu rõ khách hàng KYC và phòng chống rửa tiền AML.

Đối với doanh nghiệp, cần xem xét các vấn đề sau:

* Người tham gia phải được xác định/định dạng
* Mạng cần phải được phép
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

Hyperledger đã được kiến trúc một cách đặc biệt để có một kiến trúc mô đun. Cho dù đó là sự đồng thuận, các giao thức quản lý danh tính như LDAP hoặc OpenID Connect, các giao thức quản lý khoá hoặc thư viện mã hoá, nền tảng đã được thiết kế ở cốt lõi để được cấu hình đáp ứng các yêu cầu sử dụng của doanh nghiệp.

Ở cấp độ cao, Fabric bao gồm các thành phần mô đun sau:

* Một dịch vụ order thiết lập sự đồng thuận về thứ tự giao dịch và gửi các khối đến nút mạng.
* Một trình cung cấp dịch vụ membership chịu trách nhiệm liên kết các thực thể trong mạng với các danh tính mã hoá.
* Một dịch vụ gossip peer-to-peer tuỳ chọn để truyền các khối từ dịch vụ order tới các nút mạng khác.
* Smart contract (chaincode) chạy với môi trường container (ví dụ Docker) để cách ly. Chúng có thể được viết bằng các ngôn ngữ lập trình tiêu chuẩn nhưng không có quyền truy cập trực tiếp vào trạng thái sổ cái.
* Sổ cái có thể được cấu hình để hỗ trợ nhiều loại DBMS khác nhau.
* Chứng thực và chính sách xác thực có thể được cấu hình độc lập cho mỗi ứng dụng.

Có một thoả thuận công bằng trong ngành là không "có một blockchain nào thống trị tất cả". Hyperledger có thể được cấu hình theo nhiều cách để đáp ứng các yêu cầu giải pháp đa dạng cho nhiều trường hợp.

## **Permissioned so với Permissionless**

Trong một blockchain không được phép, hầu như ai cũng có thể tham gia và mọi người tham gia đều ẩn danh. Trong bối cảnh như vậy, không thể có sự tin tưởng nào khác ngoài trạng thái của blockchain, trước một độ sâu nhất định là bất biến. Để giảm thiểu sự thiếu tin tưởng này các blockchain không được phép thường sử dụng một loại tiền mã hoá hoặc phí giao dịch để cung cấp động lực kinh tế để bù đắp chi phí bất thường khi tham gia vào một hình thức đồng thuận chịu lỗi byzantine dựa trên bằng chứng về công việc (PoW).

Blockchain được phép, là một mặt khác, vận hành blockchain giữa một nhóm người tham gia đã biết, được định danh và thường được kiểm duyệt theo mô hình quản trị mang lại một mức độ tin cậy nhất định. Một blockchain được phép cung cấp một cách để đảm bảo các tương tác giữa một nhóm các thực thể có một mục tiêu chung nhưng có thể không hoàn toàn tin tưởng lẫn nhau. Bằng cách dựa vào danh tính của những người tham gia, một blockchain được phép có thể sử dụng các giao thức đồng thuận chịu lỗi truyền thống (CFT) hoặc byzantine (BFT) không yêu cầu khai thác tốn kém.

Ngoài ra, trong bối cảnh được phép như vậy, nguy cơ người tham gia cố tình giới thiệu mã độc thông qua hợp đồng thông minh sẽ giảm bớt. Đầu tiên, những người tham gia được biết đến với nhau và tất cả các hành động, cho dù gửi giao dịch ứng dụng, sửa đổi cấu hình của mạng hoặc triển khai hợp đồng thông minh đều được ghi lại trên blockchain theo chính sách chứng thực được thiết lập cho mạng và loại giao dịch có liên quan. Thay vì hoàn toàn ẩn danh, bên phạm tội có thể dễ dàng được xác định và vụ việc được xử lý theo các điều khoản của mô hình quản trị.

## **Smart contract**

Hợp đồng thông minh, hay Fabric gọi là chaincode, có chức năng như một ứng dụng phân tán đáng tin cậy có được sự bảo mật/tin cậy từ blockchain và sự đồng thuận cơ bản giữa các nút. Đó là logic kinh doanh của một ứng dụng blockchain.

Có ba điểm chính áp dụng cho hợp đồng thông minh, đặc biệt là khi áp dụng cho nền tảng:

* Nhiều hợp đồng thông minh chạy đồng thời trong mạng.
* Chúng có thể được triển khai linh hoạt (trong nhiều trường hợp bởi bất kỳ ai)
* Mã ứng dụng nên được coi là không đáng tin cậy, thậm chí có thể độc hại.

Hầu hết các nền tảng blockchain có hợp đồng thông minh đều tuân theo kiến trúc **order-execute** trong đó giao thức đồng thuận:

* Xác thực và yêu cầu giao dịch sau đó truyền chúng đến tất cả các nút ngang hàng.
* Mỗi nút ngang hàng sau đó thực hiện các giao dịch tuần tự.

Kiến trúc order-execute có thể được tìm thấy trong hầu hết các hệ thống blockchain hiện có, từ các nền tảng công khai/không được phép như Ethereum (với sự đồng thuận dựa trên PoW) cho đến các nền tảng được phép như Tendermint, Chain, và Quorum.

Hợp đồng thông minh thực thi trong một blockchain hoạt động với kiến trúc order-execute phải có tính xác định; mặc khác, sự đồng thuận có thể không bao giờ đạt được. Để giải quyết vấn đề không xác định, nhiều nền tảng yêu cầu các hợp đồng thông minh phải được viết bằng ngôn ngữ không chuẩn hoặc theo miền cụ thể (như Solidity) để có thể loại bỏ các hoạt động không xác định. Điều này cản trở việc áp dụng rộng rãi vì nó yêu cầu các nhà phát triển viết hợp đồng thông minh học ngôn ngữ lập trình mới và có thể dẫn đến lỗi lập trình.

Hơn nữa, vì tất cả các giao dịch được thực hiện tuần tự bởi tất cả các nút, hiệu suất và quy mô bị hạn chế. Thực tế là mã hợp đồng thông minh thực thi trên mọi nút trong hệ thống đòi hỏi phải thực hiện các biện pháp phức tạp để bảo vệ hệ thống tổng thể khỏi các hợp đồng độc hại tiềm ẩn nhằm đảm bảo khả năng phục hồi toàn bộ hệ thống.

## **Cách tiếp cận mới**

Fabric giới thiệu một kiến trúc mới cho giao dịch gọi là **excute-order-validate**. Nó giải quyết các thách thức về khả năng phục hồi, tính linh hoạt, khả năng mở rộng, hiệu suất và bảo mật mà mô hình order-execute phải đối mặt bằng cách tách luồng giao dịch thành ba bước:

* execute: thực thi giao dịch và kiểm tra tính đúng đắn của nó, qua đó chứng thực nó
* order: yêu cầu giao dịch qua giao thức đồng thuận, và
* validate: xác thực các giao dịch dựa trên chính sách chứng thực dành riêng cho ứng dụng trước khi đưa nó vào sổ cái

Thiết kế này, bắt đầu từ mô hình order-excute trong đó Fabric thực hiện các giao dịch trước khi đạt thoả thuận cuối cùng về yêu cầu của chúng.

Trong fabric, chính sách chứng thực dành riêng cho ứng dụng chỉ định các nút ngang hàng nào, hoặc bao nhiêu trong số chúng, cần phải chứng minh cho việc thực hiện đúng hợp đồng thông minh nhất định. Do đó mỗi giao dịch chỉ cần được thực hiện (xác nhận) bởi tập con của các nút ngang hàng cần thiết để đáp ứng chính sách chứng thực của giao dịch. Điều này cho phép thực hiện song song tăng hiệu suất và quy mô tổng thể của hệ thống. Giai đoạn đầu tiên nào cũng loại bỏ bất kỳ sự không xác định nào, vì các kết quả không nhất quán có thể được lọc ra trước khi yêu cầu.

Vì đã loại bỏ tính không xác định, Fabric là công nghệ blockchain đầu tiên cho phép sử dụng các ngôn ngữ lập trình tiêu chuẩn. 

## **Sự riêng tư và bảo mật**

Như đã thảo luận, trong một mạng blockchain công khai, không được phép mà sử dụng PoW cho mô hình đồng thuận, các giao dịch được thực hiện trên mọi nút. Điều này có nghĩa là bản thân các hợp đồng cũng không thể bảo mật dữ liệu giao dịch mà chúng sử lý. Mọi giao dịch và mã thực hiện nó đều hiển thị cho mọi nút trong mạng. Trong trường hợp này, chúng ta đã trao đổi tính bảo mật của hợp đồng và dữ liệu cho sự đồng thuận do PoW cung cấp.

Sự thiếu bảo mật này có thể là vấn đề đối với nhiều nghiệp vụ kinh doanh/doanh nghiệp. Ví dụ: trong một mạng lưới các đối tác trong chuỗi cung ứng, một số người tiêu dùng có thể được ưu tiên như một phương tiện để củng cố mối quan hệ hoặc thúc đẩy doanh số bán hàng bổ sung. Nếu mọi người tham gia có thể thấy mọi hợp đồng và giao dịch, việc duy trì các mối quan hệ kinh doanh đó trong một mạng lưới hoàn toàn minh bạch - mọi người sẽ muốn có mức giá ưu đãi!

Ví dụ thứ hai, hãy xem xét ngành chứng khoán, nơi một người giao dịch nắm giữ một loại chứng khoán (hoặc xử lý) sẽ không muốn các đối thủ của mình biết điều này, nếu không họ sẽ tìm cách tham gia vào trò chơi, làm suy yếu người giao dịch.

Để giải quyết sự thiếu riêng tư và bảo mật cho các mục đích theo yêu cầu của doanh nghiệp, các nền tảng blockchain đã áp dụng nhiều cách tiếp cận khác nhau. Tất cả đều có sự đánh đổi của họ.

Mã hoá dữ liệu là một cách tiếp cận để cung cấp bảo mật; tuy nhiên, trong một mạng không được phép mà sử dụng PoW cho đồng thuận, dữ liệu được mã hoá nằm trên mỗi nút. Nếu đủ thời gian và tài nguyên tính toán, mã hoá có thể bị phá vỡ. Đối với nhiều trường hợp, rủi ro thông tin của doanh nghiệp bị xâm phạm là điều không thể chấp nhận được.

Bằng chứng Zero knowledge (ZKP) là một lĩnh vực nghiên cứu khác đang được khám phá để giải quyết vấn đề này, sự đánh đổi ở đây là, hiện tại, việc tính toán ZKP đòi hỏi thời gian và nguồn lực tính toán đáng kể. Do đó, sự đánh đổi trong trường hợp này là hiệu suất để bảo mật.

Trong ngữ cảnh được phép (permissioned) có thể thúc đẩy các hình thức đồng thuận thay thế, người ta có thể khám phá ra các phương pháp hạn chế phân phối thông tin bí mật dành riêng cho các nút được uỷ quyền.

Hyperledger Fabric, là một nền tảng cho phép, cho phép bảo mật thông qua kiến trúc channel. Về cơ bản, những người tham gia trên mạng Fabric có thể thiết lập một "kênh" giữa các nhóm người tham gia nên được cấp khả năng hiển thị cho một nhóm giao dịch cụ thể. Hãy nghĩ điều này như một lớp phủ mạng. Chỉ những nút tham gia vào kênh mới có quyền truy cập vào hợp đồng thông minh (chaincode) và dữ liệu được giao dịch, giữ sự riêng tư và bảo mật.

Để cải thiện sự riêng tư và khả năng bảo mật của mình, Fabric đã bổ sung hỗ trợ cho dữ liệu riêng tư và đang nghiên cứu các bằng chứng Zero knowledge (ZKP) trong tương lai. 

## **Đồng thuận**

Yêu cầu của các giao dịch được uỷ quyền cho một thành phần mô đun của đồng thuận được tách rời khỏi các nút mạng thực hiện giao dịch và duy trì sổ cái. Cụ thể là dịch vụ yêu cầu. Vì đồng thuận là một mô đun, việc triển khai có thể được điều chỉnh theo giả định tin cậy một triển khai hoặc giải pháp cụ thể. Kiến trúc mô đun này cho phép nền tảng dựa vào các bộ công cụ được thiết lập tốt cho CFT (crash fault-tolerant) BFT (byzantine fault-tolerant) hoặc để thực hiện yêu cầu.

Trong các bản phát hành hiện có (1.0, 1.1), Fabric cung cấp dịch vụ yêu cầu CFT được triển khai với Kafka và Zookeeper. Trong các phiên bản tiếp theo, Fabric sẽ cung cấp dịch vụ yêu cầu đồng thuận Raft được triển khai với etcd/Raft và dịch vụ yêu cầu BFT phi tập trung hoàn toàn.

Lưu ý rằng ở đây không có sự loại trừ lẫn nhau, mạng Fabric có thể có nhiều dịch vụ yêu cầu hỗ trợ các ứng dụng hoặc yêu cầu các ứng dụng khác nhau.




















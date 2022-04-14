<h1> Network Monitor </h1>

<h2> Mục lục </h2>

- [1. Giám sát mạng là gì](#1-giám-sát-mạng-là-gì)
- [2. Các loại giám sát](#2-các-loại-giám-sát)
  - [2.1. Giám sát mạng (Network monitoring)](#21-giám-sát-mạng-network-monitoring)
  - [2.2 Route analytics (Phân tích tuyến đường)](#22-route-analytics-phân-tích-tuyến-đường)
  - [2.3 Website monitoring](#23-website-monitoring)
- [3. Thông tin thêm](#3-thông-tin-thêm)
  - [3.1 Có hai loại ứng dụng giám sát.](#31-có-hai-loại-ứng-dụng-giám-sát)
  - [3.2 Giám sát dựa trên Agent (Agent-based)](#32-giám-sát-dựa-trên-agent-agent-based)
  - [3.3 Không có Agent (Agentless)](#33-không-có-agent-agentless)
  - [3.4 Khuyến nghị](#34-khuyến-nghị)
- [Tài liệu tham khảo](#tài-liệu-tham-khảo)

# 1. Giám sát mạng là gì

Giám sát mạng là một t thống cho biết:
- Hiệu suất mạng chậm
- Mạng không hoạt động
- Các thiết bị làm việc

Dựa trên: Phân tích
- Thông lượng 
- Tỷ lệ lỗi
- Mất gói và delay
- Tính khả dụng của router và switch
- Thời gian phản hồi

Khi lỗi xảy ra: Quản trị viên mạng nhận được thông báo về lỗi thông qua:
- Biểu ngữ cảnh báo
- email
- điện thoại
- ...

Vai trò chiến lược trong các doanh nghiệp:
- Tối ưu hoá luồng dữ liệu
- Phát hiện thiết bị không đáng tin cậy
- Xác minh năng lực, các điều kiện của các thiết bị:
	+ Nhiệt độ
	+ tỷ lệ sử dụng

Kết luận: Mạng giám sát giúp
- Tối đa hoá hiệu suất mạng
- Giảm các lỗi tiềm ẩn của mạng

Lợi ích của doanh nghiệp khi mạng được tối ưu hoá:
- Giảm chi phí cấu trúc cơ sở hạ tầng
- Năng suất của nhân viên
- Năng suất và luồng dữ liệu nhanh chóng, đáng tin cậy.

Sự hiểu lầm phổ biến:
- Giám sát mạng không cung cấp kiểm tra bảo mật và ngăn chặn truy cập trái phép vào mạng
- Đối với loại giám sát an ninh này, hệ thống ngăn chặn xâm nhập (IPS) hoặc Hệ thống phát hiện xâm nhập (IDS) được sử dụng.
- Mạng giám sát chỉ được sử dụng để:
	+ Network utilization (sử dụng mạng)
	+ Giám sát độ tin cậy (reliability monitoring)

# 2. Các loại giám sát

Các công cụ giám sát cung cấp 1 loạt các hoạt động quét và phân tích cho các loại thiết bị và dịch vụ khác nhau. Bằng cách:
- Sử dụng các loại giao thức khác nhau trên các lớp OSI khác nhau

## 2.1. Giám sát mạng (Network monitoring)
- Được sử dụng để đo tổng thể hiệu suất mạng
- Phép đo được thực hiện bằng cách so sánh số lượng gói tin được truyền và nhận.
- Trong quá trình đó:
	+ Số lượng hop (số lượng thiết bị trung gian để đến đích) được đo
	+ Ngoài ra, độ trễ lan truyền đường dẫn và độ trễ thiết bị mạng cũng được đo lường.

Từ đó:
- Có thể ước tính mất gói, băng thông và độ trễ.
=> Làm tăng chất lượng dịch vụ trong mạng

## 2.2 Route analytics (Phân tích tuyến đường)
- Đây là một phần thiết yếu của việc giám sát.
- Là một tập hợp các công cụ, kỹ thuật và thuật ngữ giám sát việc định tuyến bên trong mạng.
- Nó hoạt động trên lớp mạng
- Phân tích định tuyến là thụ động ngang hàng (peer) và giám sát giao thức định tuyến OSPF, IS-IS, EIGRP và BGP.

Kết quả:
- Nó nhận mọi thông báo cập nhật như tất cả các router khác (ngang hàng)
- Ngoài ra, nó sử dụng dụng thuật toán Dijkstra tính toán một sơ đồ cấu trúc liên kết mạng (topology map) hoàn chỉnh, bao gồm tất cả các đườn dẫn (path).
- Hơn thế nữa, nó ghi lại lịch sử sự kiện định tuyến hoàn chỉnh có thể sử dụng sau này để khắc phục sự cố.

Nhìn chung: Phân tích tuyến đường làm:
- Tăng tốc độ, hiệu quả của mạng
- Cũng giúp cắt giảm chi phí và tăng năng suất của nhân viên.

## 2.3 Website monitoring
- Giám sát cung cấp trạng thái máy chủ:
    - Đo tính khả dụng (availability)
    - Hiệu suất (performance)
    - Kết nối (connectivity)
    - Thời gian hoạt động(uptime)
    - Bản ghi DNS (DNS records)
    - Băng thông (Bandwidth)
    - Tài nguyên phần cứng (hardware resources)

- Có 2 loại giám sát trang web:
    - Nội bộ (internal) 
    - Bên ngoài (external)

- Giám sát nội bộ (bên trong tường lửa của công ty) chịu trách nhiệm phát hiện các vấn đề liên quan đến cơ sở hạ tầng nội bộ hoặc thiết kế các ứng dụng. 
- Giám sát bên ngoài (bên ngoài tường lửa của công ty) chịu trách nhiệm giám sát end-to-end. 
- Website monitoring chịu trách nhiệm về các giao thức Internet này: 
  - HTTP (Hypertext Transfer Protocol)
  - HTTPS (Hypertext Transfer Protocol Secure)
  - FTP (File Transfer Protocol)
  - SNMP (Simple Network Monitoring Protocol)
  - SSH (Secure Socket Shell)
  - TELNET
  - POP3 (Post Office Protocol version 3)
  - DNS (Domain Name System)
  - SSL (Secure Sockets Layer)
  - TCP (Transmission Control Protocol)
  - UDP (User Datagram Protocol)

Với việc sử dụng các công cụ giám sát mạng, các quản trị viên mạng được giải phóng khỏi công việc thường ngày và có thể tập trung vào các nhiệm vụ quan trọng hơn. 
- Họ sẽ có một bức tranh đầy đủ về xử lý mạng tại thời điểm chính xác. 
- Ngoài ra, việc khắc phục sự cố thường xuyên có thể được nguyên tử hóa bằng script đặc biệt. 
- Sẽ dễ dàng hơn đáng kể do chẩn đoán chi tiết của vấn đề hỏng hóc khi khắc phục sự cố thủ công.

# 3. Thông tin thêm
## 3.1 Có hai loại ứng dụng giám sát.
- Công cụ giám sát bằng mã nguồn mở. 
  - Thông thường được phát hành theo giấy phép GPLv2
  - Các nhà phát triển bên thứ ba được phép thực hiện các thay đổi ở cấp độ mã. 
- Các công cụ giám sát độc quyền. 
  - Giấy phép hạn chế thực hiện bất kỳ loại sửa đổi nào ở cấp độ mã.

## 3.2 Giám sát dựa trên Agent (Agent-based)
- Giám sát Agent-based bao gồm một phần mềm được gọi là Agent
- Agent là một ứng dụng được cài đặt cục bộ trên máy chủ và các thiết bị mạng khác. 
- Mục tiêu của nó là giám sát hiệu suất mạng. Nếu một số lỗi xảy ra, một thông báo cảnh báo sẽ được tạo. 
- Ngoài ra,Agent có thể khắc phục một số lỗi.
- Agent là một ứng dụng nhẹ. Tuy nhiên, một số trong số chúng có thể tiêu tốn nhiều mạng tài nguyên. Đó là tại sao tác nhân nhẹ ( lightweight agent) hay còn gọi là tác nhân "vô hình" ("invisible" agent) đang trở nên phổ biến hiện nay.
- Ưu điểm chính của nó so với kiểu truyền thống là không ảnh hưởng đến hiệu suất mạng và vẫn đáp ứng hiệu suất giám sát.
- Lợi ích chính:
  - Nó cung cấp phân tích mạng sâu hơn. 
  - Thậm chí có thể chẩn đoán hiệu suất phần cứng. 
  - Nó cung cấp cũng như khả năng cảnh báo và báo cáo. 
  - Một số lỗi có thể được tự động khắc phục sự cố.
- Nhược điểm chính
  - Việc triển khai hệ thống là một quá trình tốn thời gian trong đó nhiều chi tiết của mạng cần được tính đến. 
  - Ngoài ra, các Agent cần được cập nhật.
  - Có chi phí cao hơn đáng kể (cho giấy phép).

## 3.3 Không có Agent (Agentless)
- Agentless là một giải pháp không yêu cầu bất kỳ cài đặt Agent riêng biệt nào. 
- Phân tích mạng dựa trên việc giám sát gói tin trực tiếp. 
- Nó được sử dụng để theo dõi tính khả dụng và hiệu suất của mạng.
- Tuy nhiên, nó không cung cấp bất kỳ thông tin chi tiết nào về sự cố.
- Giám sát Agentless thường dựa trên SNMP (Giao thức giám sát mạng đơn giản - Simple Network Monitoring Protocol) hoặc WMI (Công cụ quản lý Windows - Windows Management Instrumentation). Nó dựa trên một trạm quản lý trung tâm giám sát tất cả các thiết bị mạng khác. 
- Tuy nhiên, các giải pháp Agent-based cung cấp các số liệu sâu hơn.
- Ưu điểm chính:
  - Không cần Agent
  - Quá trình triển khai dễ dàng hơn. 

## 3.4 Khuyến nghị 

Sử dụng giám sát Agent-based trong các mạng lớn với cơ sở hạ tầng phức tạp:
- Nếu một lỗi xảy ra, các công cụ giám sát Agent-based sẽ cảnh báo về lỗi. 
- Nọ cũng sẽ cố gắng giải quyết vấn đề một cách tự động. 
- Nếu có một lỗi cần phải có sự chú ý của các quản trị viên mạng. Một công cụ giám sát dựa trên Agent sẽ cung cấp chi tiết thông tin về nơi và loại vấn đề đã xảy ra. Khiến việc tìm kiếm và thay thế một lỗi hỏng đòi hỏi ít thời gian hơn.

Giám sát Agentless thích hợp hơn trong các mạng quy mô nhỏ bao gồm ít thiết bị mạng:
- Chỉ cần giám sát tính khả dụng và hiệu suất của mạng. 
- Ở đó không cần thông tin chi tiết về các chỉ số và thông báo của các thiết bị mạng trong các loại mạng này.

Khuyến nghị sử dụng cả giám sát mạng Agent-based và Agentless:
- Các nhà cung cấp như Nagios hoặc Zabbix cung cấp cả khả năng dựa trên Agent và không có Agent trong các giải pháp.
  - Các phần thiết yếu của mạng, nơi ưu tiên tính khả dụng và hiệu suất, giám sát dựa trên Agent có thể được sử dụng. 
  - Đối với các phần ít quan trọng hơn của mạng không có Agent là thích hơn.

Một giải pháp giám sát kết hợp có những lợi thế của từng loại. 
- Giúp ưu tiên các bộ phận quan trọng hơn cần được theo dõi chi tiết. Điều này sẽ làm tăng hiệu suất mạng. 
- Ngoài ra, chỉ những thông tin quan trọng mới được báo cáo.

# Tài liệu tham khảo

1. https://core.ac.uk/download/pdf/38124402.pdf
<h1> Tổng quan về Zabbix 6.0 </h1>

<h2> Mục lục </h2>

- [1. Zabbix là gì](#1-zabbix-là-gì)
- [2. Lịch sử phát triển và các phiên bản](#2-lịch-sử-phát-triển-và-các-phiên-bản)
  - [2.1 Lịch sử phát triển](#21-lịch-sử-phát-triển)
  - [2.2 Vòng đời phát triển](#22-vòng-đời-phát-triển)
- [3. Các tính năng của Zabbix](#3-các-tính-năng-của-zabbix)
- [Tài liệu tham khảo](#tài-liệu-tham-khảo)

# 1. Zabbix là gì
- Zabbix là một giải pháp giám sát phân tán mã nguồn mở cấp doanh nghiệp.
- Zabbix được tạo ra bởi Alexei Vladishev và hiện đang được Zabbix SIA phát triển và hỗ trợ.
- Zabbix là một phần mềm giám sát nhiều thông số của mạng cũng như tình trạng và tính toàn vẹn của máy chủ, máy ảo, ứng dụng, dịch vụ, cơ sở dữ liệu, trang web, đám mây,...
- Zabbix sử dụng cơ chế thông báo linh hoạt cho phép người dùng định cấu hình cảnh báo dựa trên e-mail cho hầu như mọi sự kiện. Điều này cho phép phản ứng nhanh với các sự cố máy chủ. 

- Tất cả các báo cáo và thống kê của Zabbix, cũng như các thông số cấu hình, đều được truy cập thông qua giao diện người dùng dựa trên web. Giao diện người dùng dựa trên web đảm bảo rằng trạng thái của mạng và tình trạng của máy chủ có thể được đánh giá từ bất kỳ vị trí nào.
- Zabbix là phần mềm miễn phí, được phát hành theo GPL Giấy phép Công cộng phiên bản 2 (General Public License version 2).
# 2. Lịch sử phát triển và các phiên bản
## 2.1 Lịch sử phát triển
- Zabbix được thành lập vào năm 1998. Đây là dự án công ty của Alexei Vladishev. 
  - Khi đó, ông đang là nhân viên quản trị hệ thống trong một ngân hàng chịu trách nhiệm quản lý cơ sở dữ liệu. 
  - Để tự động hóa công việc thường ngày, ông Vladishev đã tạo ra một nguyên mẫu đầu tiên của Zabbix. Nó dựa trên tập lệnh Perl. (Vladishev 2004.) 
  - Vào thời điểm đó chỉ có hai người chơi trên thị trường đó là HP Open View và IBM BMC. Tuy nhiên, những giải pháp này quá đắt và quá khó để bảo trì và cấu hình. 
- Phải mất ba năm để phát hành phiên bản công khai đầu tiên của Zabbix, **Zabbix v1.0 alpha 1** được phát hành vào năm 2001  theo General Public License (GPL). 
- Năm 2004 Zabbix v1 phiên bản Hỗ trợ Dài hạn (Long Term Support - LTS) đầu tiên được phát hành.
- Tiếp theo là các phiên bản:
  - Zabbix 2.0 LTS (21/05/2012), 
  - Zabbix 2.2 LTS (12/11/2013), 
  - Zabbix 3.0 LTS (16/02/2016), 
  - Zabbix 3.4 (8/2017)  
  - Zabbix 4.0 LTS (1/10/2018), 
  - Zabbix 5.0 LTS (12/5/2020), 
  - Zabbix 5.4 (17/5/2021), 
  - Zabbix 6.0 LTS (8/02/2022)

- Đang phát triển Zabbix 6.2

## 2.2 Vòng đời phát triển

![Imgur](https://i.imgur.com/tmaVCj1.png)

Trong mỗi năm rưỡi (1,5) Zabbix sẽ phát hành:
- **Zabbix LTS (Long Term Support)**:
  - Các bản phát hành Zabbix LTS hỗ trợ cho khách hàng trong 5 năm
  - 3 năm Full Support - hỗ trợ khắc phục các vấn đề chung, quan trọng và bảo mật
  - Thêm 2 năm Limited Support - chỉ hỗ trợ các vấn đề quan trọng và bảo mật

![Imgur](https://i.imgur.com/iCVaHBU.png)

- **Zabbix Standard**:
  - Các bản phát hành Zabbix Standard hỗ trợ cho khách hàng trong sáu tháng Full Support (các vấn đề chung, quan trọng và bảo mật) cho đến khi phát hành ổn định Zabbix tiếp theo.
  - Thêm một (1) tháng Limited Support (chỉ các vấn đề quan trọng và bảo mật).

![Imgur](https://i.imgur.com/IkVegnI.png)

<h3>Các bản phát hành được hỗ trợ hiện tại</h3>

![Imgur](https://i.imgur.com/MlinTKK.png)

# 3. Các tính năng của Zabbix

Zabbix:
- Một giải pháp giám sát mạng tích hợp cao
- Cung cấp nhiều tính năng trong một gói duy nhất.

<h3>Thu thập dữ liệu</h3>

- Kiểm tra tính khả dụng và hiệu suất
- Hỗ trợ SNMP, IPMI, JMX, giám sát VMware
- Kiểm tra tùy chỉnh
- Thu thập dữ liệu mong muốn ở các khoảng thời gian tùy chỉnh
- Được thực hiện bởi server/proxy và bởi các Agent

<h3>Định nghĩa ngưỡng linh hoạt</h3>

- Có thể xác định các ngưỡng sự cố rất linh hoạt, được gọi là trình kích hoạt (triggers), tham chiếu các giá trị từ cơ sở dữ liệu phụ trợ (backend database)

<h3>Cảnh báo có thể cấu hình cao</h3>

- Có thể được tùy chỉnh gửi thông báo cho lịch trình báo cáo, người nhận, loại phương tiện (media type)

<h3>Vẽ đồ thị thời gian thực</h3>

- Các mục (items) được giám sát ngay lập tức được lập biểu đồ bằng cách sử dụng chức năng vẽ đồ thị tích hợp (built-in graphing functionality)

<h3>Khả năng giám sát web</h3>

- Zabbix có thể theo dõi đường dẫn (path) của những cú click chuột trên một trang web và kiểm tra chức năng, thời gian phản hồi

<h3>Các tùy chọn hình ảnh hóa mở rộng</h3>

- Khả năng tạo các biểu đồ tùy chỉnh có thể kết hợp nhiều mục vào một chế độ xem duy nhất
- Bản đồ mạng (network maps)
- Trình chiếu tổng quan kiểu bảng điều khiển
- Báo cáo
- Chế độ xem high-level (business) của các tài nguyên được giám sát

<h3>Lưu trữ dữ liệu lịch sử</h3>

- Dữ liệu được lưu trữ trong cơ sở dữ liệu
- Lịch sử có thể định cấu hình
- Tích hợp sẵn quy trình dọn dẹp

<h3>Cấu hình dễ dàng</h3>

- Thêm các thiết bị được giám sát làm máy chủ (host)
- Hosts được chọn để theo dõi, một khi trong cơ sở dữ liệu
- Áp dụng các mẫu (templates) cho các thiết bị được giám sát

<h3>Sử dụng các template</h3>

- Grouping checks in templates (Nhóm lại các check trong các template)
- Các template có thể kế thừa từ các template khác

<h3>Network discovery</h3>

- Tự động khám phá các thiết bị mạng
- Tự động đăng ký Agent
- Khám phá file system, network interfaces và SNMP OIDs

<h3>Giao diện web nhanh</h3>

- Sử dụng PHP xây dựng một giao diện người dùng dựa trên web
- Có thể truy cập từ mọi nơi
- audit log

<h3>API Zabbix</h3>

- Zabbix API cung cấp giao diện lập trình cho Zabbix để thao tác hàng loạt, tích hợp phần mềm của bên thứ 3 (3rd party software integration) và các mục đích khác.

<h3>Hệ thống quyền</h3>

- Xác thực người dùng an toàn
- Phân quyền người dùng

<h3>Agent có đầy đủ tính năng và dễ dàng mở rộng</h3>

- Triển khai trên các mục tiêu giám sát
- Có thể được triển khai trên cả Linux và Windows

<h3>Binary daemons</h3>

- Được viết bằng C, cho hiệu suất và diện tích bộ nhớ nhỏ
- Dễ dàng di chuyển

<h3>Sẵn sàng cho các môi trường phức tạp</h3>

- Giám sát từ xa dễ dàng bằng cách sử dụng proxy Zabbix


# Tài liệu tham khảo

1. [What is Zabbix](https://www.zabbix.com/documentation/current/en/manual/introduction/about)
2. [Zabbix Life Cycle & Release Policy](https://www.zabbix.com/life_cycle_and_release_policy)
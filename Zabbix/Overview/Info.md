<h1> Tổng quan về Zabbix 6.0 </h1>

<h2> Mục lục </h2>

- [1. Zabbix là gì](#1-zabbix-là-gì)
- [2. Lịch sử phát triển và các phiên bản](#2-lịch-sử-phát-triển-và-các-phiên-bản)
  - [2.1 Lịch sử phát triển](#21-lịch-sử-phát-triển)
  - [2.2 Vòng đời phát triển](#22-vòng-đời-phát-triển)
- [3. Các tính năng của Zabbix](#3-các-tính-năng-của-zabbix)
- [4. Architecture](#4-architecture)
- [5. Ưu điểm của Zabbix](#5-ưu-điểm-của-zabbix)
- [6. Những điều cải thiện](#6-những-điều-cải-thiện)
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
- Cung cấp nhiều tính năng trong một gói duy nhất:
  - Giám sát lên đến hàng nghìn nút
  - Giám sát file log
  - Tạo báo cáo qua email, điện thoại,...
  - Quản lý mẫu (template)
  - Vẽ đồ thị thời gian thực

<h3>Thu thập dữ liệu</h3>

- Thu thập dữ liệu từ bất kỳ nguồn nào
  - Thiết bị mạng
  - Cloud services, Virtual machines
  - Giám sát mức hệ điều hành
  - File log
  - Cơ sở dữ liệu
  - Các ứng dụng
  - Giám sát trang web
  - Thu thập dữ liệu từ các điểm cuối (end-points) API bên ngoài

![Imgur](https://i.imgur.com/nu9BlVX.png)

- Tuỳ chỉnh thu thập dữ liệu:
  - Sử dụng phương pháp đẩy và kéo để thu thập dữ liệu
  - Thu thập dữ liệu từ bất kỳ loại nào:
    - Số
    - Văn bản
    - Nhị phân
    - JSON có cấu trúc, XML, CSV và các định dạng dữ liệu khác
  - Thu thập dữ liệu mong muốn ở các khoảng thời gian tùy chỉnh
    - Lập lịch thu thập số liệu
    - Điều chỉnh dữ liệu để giám sát tần số cao
  - Theo dõi file log:
    - Thu thập và lọc các mục (entry) trong file log
    - Truy xuất số lượng mục nhập (entry) trong file log

![Imgur](https://i.imgur.com/7LprwW7.png)


<h3>Định nghĩa ngưỡng linh hoạt</h3>

- Có thể xác định các ngưỡng sự cố rất linh hoạt, được gọi là trình kích hoạt (triggers), tham chiếu các giá trị từ cơ sở dữ liệu phụ trợ (backend database)

<h3>Cấu hình cảnh báo</h3>

- Có thể được tùy chỉnh gửi thông báo cho lịch trình báo cáo, người nhận, loại phương tiện (media type)

<h3>Đồ thị thời gian thực</h3>

- Các mục (items) được giám sát ngay lập tức được lập biểu đồ bằng cách sử dụng chức năng vẽ đồ thị tích hợp (built-in graphing functionality)

![Imgur](https://i.imgur.com/seA19wH.png)

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

# 4. Architecture

![Imgur](https://i.imgur.com/In7vhDD.png)

<h3>Server</h3>

- Server Zabbix là thành phần trung tâm mà các Agent báo cáo thông tin và thống kê về tính khả dụng và tính toàn vẹn. 
- Server là kho lưu trữ trung tâm, trong đó tất cả dữ liệu cấu hình, thống kê và hoạt động được lưu trữ.
- Sử dụng để giám sát, nhận dữ liệu theo lịch, xử lý, phân tích vào thông báo dữ liệu.
- Nếu xảy ra lỗi, server Zabbix sẽ cảnh báo người quản trị.

<h3>Database storage</h3>

- Nơi lưu trữ tất cả thông tin cấu hình, dữ liệu do Zabbix thu thập
- Ví dụ: MySQL, SQLite, Oracle hoặc PostgreSQL

<h3>Web interface</h3>

- Để dễ dàng truy cập Zabbix từ mọi nơi và từ bất kỳ nền tảng nào qua web interface PHP. 
- Interface là một phần của máy chủ Zabbix và thường (nhưng không nhất thiết) chạy trên cùng một máy vật lý với máy server.

<h3>Proxy</h3>

- Zabbix proxy có thể thu thập dữ liệu hiệu suất và tính khả dụng thay mặt cho máy chủ Zabbix. 
- Tất cả các dữ liệu thu thập được sẽ được chuyển tiếp đến server Zabbix.
- Proxy là một phần tùy chọn của việc triển khai Zabbix

<h3>Agent</h3>

- Các Agent Zabbix được triển khai trên các mục tiêu giám sát để chủ động giám sát các tài nguyên và ứng dụng máy khách 
- Báo cáo dữ liệu thu thập được cho máy chủ Zabbix. 
- Kể từ Zabbix 4.4, có hai loại Agent có sẵn: 
  - Agent Zabbix (nhẹ, được hỗ trợ trên nhiều nền tảng, được viết bằng C) 
  - và Agent Zabbix 2 (cực kỳ linh hoạt, có thể mở rộng dễ dàng với các plugin, được viết bằng Go).

# 5. Ưu điểm của Zabbix
- Giám sát cả Server và thiết bị mạng
- Cấu hình thông qua giao diện web dễ dàng
- Hỗ trợ máy chủ Linux,...
- Thông báo sự cố qua email, ...
- Biểu đồ theo dõi và báo cáo
- Mã nguồn mở

# 6. Những điều cải thiện
- Thiết kế lại hoàn toàn phần Services
  - Cải thiện hiện thị trạng thái và mức SLA hiện tại của các dịch vụ
![Imgur](https://i.imgur.com/nmXD7ut.png)

- Theo dõi trạng thái nút cụm trong tiện ích con `System information`
![Imgur](https://i.imgur.com/TfXh1kg.png)

- Cập nhật thêm nhiều mẫu mới (Templates)
![Imgur](https://i.imgur.com/dP9vTOq.png)

- Thiết kế lại Audit log cho phép cấp độ chi tiết mới, tuỳ chọn lọc được cải thiện
![Imgur](https://i.imgur.com/qeOalHR.png)

- Tiện ích mới cung cấp nhiều cách để hiển thị các chỉ số và cơ sở hạ tầng đã thu thập:
![Imgur](https://i.imgur.com/WN9QjO5.png)

- Cải thiện hiệu suất
  - Cải thiện hiệu suất proxy Zabbix, sử dụng bộ nhớ, máy chủ và giao diện người dùng.
  - Giảm kích thước bảng lịch sử
# Tài liệu tham khảo

1. [What is Zabbix](https://www.zabbix.com/documentation/current/en/manual/introduction/about)
2. [Zabbix Life Cycle & Release Policy](https://www.zabbix.com/life_cycle_and_release_policy)
3. [Explore Zabbix features](https://www.zabbix.com/features#problem_detection)
4. https://docero.tips/download/mastering-zabbix-kq6wy3qq87?hash=7b049164e2754d557b9550a095c754f2
5. https://media.oiipdf.com/pdf/1bdda601-c6a3-40be-9d51-92af5d8a6704.pdf
6. https://www.theseus.fi/bitstream/handle/10024/120834/Mikhail_Sharin.pdf?sequence=1&isAllowed=y
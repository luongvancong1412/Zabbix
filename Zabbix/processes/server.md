<h1>Tổng quan Server Zabbix</h1>

<h2>Mục lục</h2>

- [1. Tổng quan](#1-tổng-quan)
- [2. Các thao tác quản lý](#2-các-thao-tác-quản-lý)
- [3. Server process types - Các loại quy trình máy chủ](#3-server-process-types---các-loại-quy-trình-máy-chủ)
- [Tài liệu tham khảo](#tài-liệu-tham-khảo)

# 1. Tổng quan
- Server Zabbix là process central của phần mềm Zabbix thực hiện việc:
  - Polling (thăm dò) và trapping of data (bẫy dữ liệu)
  - Tính toán các trigger
  - Gửi thông báo cho người dùng. 
- Nó là component central (thành phần trung tâm) mà các Agent Zabbix và proxy báo cáo dữ liệu về availability (tính khả dụng) và integrity (tính toàn vẹn) của hệ thống. 

- Máy chủ là repository central (kho lưu trữ trung tâm), trong đó tất cả dữ liệu cấu hình, thống kê và hoạt động được lưu trữ và chính thực thể trong Zabbix sẽ chủ động cảnh báo cho quản trị viên khi có vấn đề phát sinh trong bất kỳ hệ thống được giám sát nào.

Hoạt động của một máy chủ Zabbix cơ bản được chia thành ba thành phần riêng biệt:
- Zabbix server
- Web frontend
- Database storage

# 2. Các thao tác quản lý

<h3> Nếu được cài đặt dưới dạng gói </h3>

- Khởi động server (hoạt động trên hầu hết các hệ thống GNU / Linux):
```
shell> service zabbix-server start
```
- Trên các hệ thống khác, có thể cần chạy:
```
shell> /etc/init.d/zabbix-server start
```
- Dừng:
```
shell> service zabbix-server stop
```
- Khởi động lại:
```
shell> service zabbix-server restart
```
- Xem trạng thái hoạt động:
```
shell> service zabbix-server status
```

<h3>Khởi động thủ công</h3>

- Nếu cách trên không hoạt động, phải khởi động nó theo cách thủ công. 
- Tìm đường dẫn đến tệp nhị phân zabbix_server và thực hiện:
```
shell> zabbix_server
```
Có thể sử dụng các tham số dòng lệnh sau với máy chủ Zabbix:

```
-c --config <file>              path to the configuration file (default is /usr/local/etc/zabbix_server.conf)
-f --foreground                 run Zabbix server in foreground
-R --runtime-control <option>   perform administrative functions
-h --help                       give this help
-V --version                    display version number
```
- Ví dụ về việc chạy máy chủ Zabbix với các tham số dòng lệnh:
```
shell> zabbix_server -c /usr/local/etc/zabbix_server.conf
shell> zabbix_server --help
shell> zabbix_server -V
```

<h3> Runtime control - Kiểm soát thời gian chạy</h3>
Tùy chọn kiểm soát thời gian chạy:

STT|Option| Mô tả|Mục tiêu|
|---|---|---|---|
1|config_cache_reload|Tải lại bộ đệm cấu hình.|
2|Diaginfo [= < target >]	|Thu thập thông tin chẩn đoán trong tệp nhật ký máy chủ.|historycache - thống kê bộ đệm lịch sử . valuecache - xử lý trước thống kê bộ đệm giá trị. Alerting - thống kê trình quản lý cảnh báo. lld - thống kê trình quản lý LLD. locks - danh sách mutexes (trống trên hệ thống ** BSD *)
3|ha_status|Ghi nhật ký trạng thái High availability (HA) cluster.||	
4|ha_remove_node = target|Loại bỏ nút high availability (HA) bằng tên hoặc ID của nó.(Không thể loại bỏ các nút đang hoạt động / ở chế độ chờ.|target - tên hoặc ID của nút (có thể lấy bằng cách chạy ha_status)|
5|ha_set_failover_delay = delay|Đặt độ trễ chuyển đổi high availability (HA) failover. Các hậu tố thời gian được hỗ trợ, ví dụ: 10s, 1m.||
6|secret_reload|Tải lại secrets từ Vault.	||
7|service_cache_reload|Tải lại service manager cache.||	
8|snmp_cache_reload|Tải lại SNMP cache, clear SNMP properties - các thuộc tính SNMP (engine time - thời gian động cơ, engine boots - khởi động động cơ,engine id - id động cơ, credentials - thông tin đăng nhập) cho all host.||	
9|housekeeper_execute|	Bắt đầu thủ tục housekeeping.|	
10|trigger_housekeeper_execute|	Bắt đầu trigger housekeeping procedure.|
11|log_level_increase [= < target >]|Tăng log level, ảnh hưởng đến tất cả các quá trình (processses) nếu không chỉ định mục tiêu. Không được hỗ trợ trên hệ thống ** BSD *.|process type - Tất cả các quy trình thuộc loại được chỉ định (ví dụ: poller). See all server process types. Process type, N - Loại quy trình và số (ví dụ: poller,3). pid - Định danh quy trình (1 đến 65535). Đối với các giá trị lớn hơn, chỉ định mục tiêu là 'Process type, N'.|
|12|log_level_decrease [= < target >]|Giảm log level, ảnh hưởng đến tất cả các quá trình nếu không chỉ định mục tiêu.Không được hỗ trợ trên hệ thống ** BSD *.|



Ví dụ về việc đặt độ trễ chuyển đổi dự phòng HA tối thiểu là 10 giây:
```
zabbix_server -R ha_set_failover_delay=10s
```

<h3>Process user</h3>

- Máy chủ Zabbix được thiết kế để có thể chạy với người dùng thông thường không cần user root.

- Nếu bạn cố gắng chạy nó dưới dạng 'root', nó sẽ chuyển sang người dùng 'zabbix'
- Có thể chạy máy chủ dưới dạng 'root' nếu bạn sửa đổi tham số 'AllowRoot' trong tệp cấu hình máy chủ.

- Nếu Server và Agent Zabbix được chạy trên cùng một máy, nên sử dụng người dùng khác để chạy server chứ không phải để chạy Agent. 
- Mặt khác, nếu cả hai đều được chạy với cùng một người dùng, thì Agent có thể truy cập tệp cấu hình server và bất kỳ người dùng cấp Quản trị viên nào trong Zabbix đều có thể dễ dàng truy xuất, chẳng hạn như mật khẩu cơ sở dữ liệu.

# 3. Server process types - Các loại quy trình máy chủ
- alert manager- người quản lý hàng đợi cảnh báo
- alert syncer- cảnh báo DB writer
- alerter- quy trình gửi thông báo
- availability manager- quy trình cập nhật tính khả dụng của máy chủ
- configuration syncer- quy trình quản lý bộ nhớ đệm trong bộ nhớ của dữ liệu cấu hình
- discoverer- quy trình khám phá các thiết bị
- escalator- quy trình escalation các hành động
- history poller- quy trình xử lý các kiểm tra được tính toán và kiểm tra nội bộ yêu cầu kết nối cơ sở dữ liệu
- history syncer- lịch sử DB writer
- housekeeper- quy trình xóa dữ liệu lịch sử cũ
- http poller- poller ​​giám sát web
- icmp pinger- poller kiểm tra icmpping
- ipmi manager- poller quản lý ​​IPMI
- ipmi poller- poller kiểm tra IPMI
- java poller- poller để kiểm tra Java
- lld manager- quy trình quản lý của các nhiệm vụ khám phá low-level
- lld worker- worker process của các nhiệm vụ khám phá low-level
- odbc poller- poller để kiểm tra ODBC
- poller- người thăm dò bình thường để kiểm tra thụ động
- preprocessing manager- người quản lý các nhiệm vụ tiền xử lý
- preprocessing worker- quy trình xử lý trước dữ liệu
- problem housekeeper- quy trình để loại bỏ các vấn đề của các trình kích hoạt đã xóa
- proxy poller- poller ​​cho proxy thụ động
- report manager- người quản lý các nhiệm vụ tạo báo cáo theo lịch trình
- report writer- quy trình tạo báo cáo được lập lịch
- self-monitoring- quy trình thu thập số liệu thống kê máy chủ nội bộ
- snmp trapper- bẫy cho bẫy SNMP
- task manager- quy trình thực hiện từ xa các tác vụ do các thành phần khác yêu cầu (ví dụ: đóng vấn đề, xác nhận vấn đề, kiểm tra giá trị mục ngay bây giờ, chức năng lệnh từ xa)
- timer- hẹn giờ để xử lý các bảo trì
- trapper- trapper để kiểm tra hoạt động, bẫy, giao tiếp proxy
- unreachable poller- người thăm dò ý kiến ​​cho các thiết bị không kết nối được
- vmware collector- Bộ thu thập dữ liệu VMware chịu trách nhiệm thu thập dữ liệu từ các dịch vụ VMware

- Tệp nhật ký máy chủ có thể được sử dụng để quan sát các loại quy trình này.

Nhiều loại quy trình máy chủ Zabbix khác nhau có thể được giám sát bằng cách sử dụng mục nội bộ zabbix `[ process, <type>, <mode>, <state>]` .

<h3>Nền tảng được hỗ trợ</h3>

Máy chủ Zabbix được thử nghiệm trên các nền tảng sau:

- Linux
- Solaris
- AIX
- HP-UX
- Mac OS X
- FreeBSD
- OpenBSD
- NetBSD
- SCO Open Server
- Tru64 / OSF1

>Zabbix cũng có thể hoạt động trên các hệ điều hành giống Unix khác.
 
<h3>Ngôn ngữ</h3>
- Server yêu cầu ngôn ngữ UTF-8

# Tài liệu tham khảo

1. https://www.zabbix.com/documentation/current/en/manual/concepts/server
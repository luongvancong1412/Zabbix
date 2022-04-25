<h1> Proxy </h1>

<h2> Mục lục </h2>

- [Tổng quan](#tổng-quan)
- [Quản lý proxy](#quản-lý-proxy)
  - [Nếu được cài đặt dưới dạng gói](#nếu-được-cài-đặt-dưới-dạng-gói)
  - [Khởi động thủ công](#khởi-động-thủ-công)
  - [](#)

# Tổng quan
- Zabbix proxy là:
  - Một quy trình thu thập dữ liệu giám sát từ một hoặc nhiều thiết bị được giám sát
  - và gửi thông tin đến máy chủ Zabbix.
- Về cơ bản hoạt động thay mặt cho máy chủ. 
  - Tất cả dữ liệu thu thập được sẽ được lưu vào bộ đệm cục bộ và sau đó được chuyển đến máy chủ Zabbix mà proxy thuộc về.

- Triển khai proxy là tùy chọn, nhưng có thể rất có lợi khi phân phối tải của một máy chủ Zabbix. 
  - Nếu chỉ có proxy thu thập dữ liệu, quá trình xử lý trên server sẽ sử dụng ít CPU hơn và disk I/O hungry.

- Là giải pháp lý tưởng để giám sát tập trung các vị trí, chi nhánh và mạng từ xa mà không có quản trị viên cục bộ.

- Yêu cầu một cơ sở dữ liệu riêng biệt.
  - Cơ sở dữ liệu được hỗ trợ: 
    - SQLite
    - MySQL
    - PostgreSQL.

# Quản lý proxy

## Nếu được cài đặt dưới dạng gói

- `Khởi động` proxy trên hầu hết các hệ thống `GNU/Linux` bằng cách thực thi:
```
shell> service zabbix-proxy start
```
- Trên các hệ thống khác, có thể cần chạy:
```
shell> /etc/init.d/zabbix-proxy start
```
- Để `dừng`/`khởi động lại`/`xem trạng thái` proxy Zabbix, hãy sử dụng các lệnh sau:
```
shell> service zabbix-proxy stop
shell> service zabbix-proxy restart
shell> service zabbix-proxy status
```

## Khởi động thủ công

- Nếu cách trên không hoạt động, bạn phải khởi động nó theo cách thủ công. 
- Tìm đường dẫn đến tệp `zabbix_proxy` và thực hiện:
```
shell> zabbix_proxy
```

Các option với lệnh  zabbix_proxy:
Option|Full| Mô tả|
|:---:|:---:|---|
`-c`| `--config <file>`| Đường dẫn tới file cấu hình
`-f`|`--foreground`|Chạy zabbix proxy trong foreground (nền)
`-R`| `--runtime-control <option>`| Thực hiện các chức năng quản trị
`-h`| `--help`| Trợ giúp
`-V`| `--version`| Hiển thị số phiên bản|

Ví dụ:
```
shell> zabbix_proxy -c /usr/local/etc/zabbix_proxy.conf
shell> zabbix_proxy --help
shell> zabbix_proxy -V
```

## 
Tùy chọn kiểm soát thời gian chạy:

Lựa chọn	Sự miêu tả	Mục tiêu
config_cache_reload	Tải lại bộ đệm cấu hình. Bỏ qua nếu bộ nhớ cache hiện đang được tải.
Proxy Zabbix đang hoạt động sẽ kết nối với máy chủ Zabbix và yêu cầu dữ liệu cấu hình.	
Diaginfo [= < target >]	Thu thập thông tin chẩn đoán trong tệp nhật ký proxy.	historycache -
xử lý trước số liệu thống kê bộ đệm lịch sử -
khóa thống kê trình quản lý tiền xử lý - danh sách mutexes (trống trên hệ thống ** BSD *)
snmp_cache_reload	Tải lại bộ đệm SNMP, xóa các thuộc tính SNMP (thời gian động cơ, khởi động động cơ, id động cơ, thông tin đăng nhập) cho tất cả các máy chủ.	
housekeeper_execute	Bắt đầu thủ tục dọn phòng. Bỏ qua nếu thủ tục dọn phòng hiện đang được thực hiện.	
log_level_increase [= < target >]	Tăng mức độ nhật ký, ảnh hưởng đến tất cả các quá trình nếu mục tiêu không được chỉ định.
Không được hỗ trợ trên hệ thống ** BSD *.	loại quy trình - Tất cả các quy trình thuộc loại được chỉ định (ví dụ: thăm dò ý kiến)
Xem tất cả các loại quy trình proxy .
loại quy trình, N - Loại quy trình và số (ví dụ: poller, 3)
pid - Định danh quy trình (1 đến 65535). Đối với các giá trị lớn hơn, chỉ định mục tiêu là 'loại quy trình, N'.
log_level_decrease [= < target >]	Giảm cấp độ nhật ký, ảnh hưởng đến tất cả các quá trình nếu mục tiêu không được chỉ định.
Không được hỗ trợ trên hệ thống ** BSD *.
Ví dụ về việc sử dụng điều khiển thời gian chạy để tải lại bộ đệm ẩn cấu hình proxy:

shell> zabbix_proxy -c /usr/local/etc/zabbix_proxy.conf -R config_cache_reload
Ví dụ về việc sử dụng điều khiển thời gian chạy để thu thập thông tin chẩn đoán:

Gather all available diagnostic information in the proxy log file:
shell> zabbix_proxy -R diaginfo
Gather history cache statistics in the proxy log file:
shell> zabbix_proxy -R diaginfo=historycache
Ví dụ về việc sử dụng điều khiển thời gian chạy để tải lại bộ đệm SNMP:

shell> zabbix_proxy -R snmp_cache_reload  
Ví dụ về việc sử dụng kiểm soát thời gian chạy để kích hoạt việc thực thi quản gia

shell> zabbix_proxy -c /usr/local/etc/zabbix_proxy.conf -R housekeeper_execute
Ví dụ về việc sử dụng kiểm soát thời gian chạy để thay đổi cấp độ nhật ký:

Increase log level of all processes:
shell> zabbix_proxy -c /usr/local/etc/zabbix_proxy.conf -R log_level_increase
Increase log level of second poller process:
shell> zabbix_proxy -c /usr/local/etc/zabbix_proxy.conf -R log_level_increase=poller,2
Increase log level of process with PID 1234:
shell> zabbix_proxy -c /usr/local/etc/zabbix_proxy.conf -R log_level_increase=1234
Decrease log level of all http poller processes:
shell> zabbix_proxy -c /usr/local/etc/zabbix_proxy.conf -R log_level_decrease="http poller"
Xử lý người dùng
Zabbix proxy được thiết kế để chạy với tư cách người dùng không phải root. Nó sẽ chạy như bất kỳ người dùng không phải root nào mà nó được khởi động. Vì vậy, bạn có thể chạy proxy với tư cách là bất kỳ người dùng không phải root nào mà không gặp bất kỳ sự cố nào.

Nếu bạn cố gắng chạy nó dưới dạng 'root', nó sẽ chuyển sang người dùng 'zabbix' được mã hóa cứng, người dùng này phải có trên hệ thống của bạn. Bạn chỉ có thể chạy proxy với tư cách là 'root' nếu bạn sửa đổi tham số 'AllowRoot' trong tệp cấu hình proxy cho phù hợp.

Tập tin cấu hình
Xem các tùy chọn tệp cấu hình để biết chi tiết về cách định cấu hình zabbix_proxy.

Các loại quy trình proxy
availability manager- quy trình cập nhật tính khả dụng của máy chủ
configuration syncer- quy trình quản lý bộ nhớ đệm trong bộ nhớ của dữ liệu cấu hình
data sender- người gửi dữ liệu proxy
discoverer- quy trình khám phá các thiết bị
heartbeat sender- người gửi nhịp tim proxy
history poller- quy trình xử lý các kiểm tra được tính toán, tổng hợp và nội bộ yêu cầu kết nối cơ sở dữ liệu
history syncer- nhà văn DB lịch sử
housekeeper- quy trình xóa dữ liệu lịch sử cũ
http poller- người thăm dò ý kiến ​​giám sát web
icmp pinger- người thăm dò để kiểm tra icmpping
ipmi manager- Người quản lý cuộc thăm dò ý kiến ​​IPMI
ipmi poller- người thăm dò để kiểm tra IPMI
java poller- người thăm dò để kiểm tra Java
odbc poller- người thăm dò để kiểm tra ODBC
poller- người thăm dò bình thường để kiểm tra thụ động
preprocessing manager- người quản lý các nhiệm vụ tiền xử lý
preprocessing worker- quy trình xử lý trước dữ liệu
self-monitoring- quy trình thu thập số liệu thống kê máy chủ nội bộ
snmp trapper- bẫy cho bẫy SNMP
task manager- quy trình thực hiện từ xa các tác vụ do các thành phần khác yêu cầu (ví dụ: đóng vấn đề, xác nhận vấn đề, kiểm tra giá trị mục ngay bây giờ, chức năng lệnh từ xa)
trapper- trapper để kiểm tra hoạt động, bẫy, giao tiếp proxy
unreachable poller- người thăm dò ý kiến ​​cho các thiết bị không kết nối được
vmware collector- Bộ thu thập dữ liệu VMware chịu trách nhiệm thu thập dữ liệu từ các dịch vụ VMware
Tệp nhật ký proxy có thể được sử dụng để quan sát các loại quy trình này.

Có thể giám sát nhiều loại quy trình proxy Zabbix bằng cách sử dụng mục nội bộ zabbix [ process, <type>, <mode>, <state>] .

Nền tảng được hỗ trợ
Zabbix proxy chạy trên cùng danh sách các nền tảng được hỗ trợ # máy chủ như máy chủ Zabbix.

Ngôn ngữ
Lưu ý rằng proxy yêu cầu ngôn ngữ UTF-8 để một số mục văn bản có thể được diễn giải chính xác. Hầu hết các hệ thống giống Unix hiện đại đều có ngôn ngữ UTF-8 làm mặc định, tuy nhiên, có một số hệ thống có thể cần phải đặt cụ thể.
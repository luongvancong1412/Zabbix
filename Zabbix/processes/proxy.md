<h1> Proxy </h1>

<h2> Mục lục </h2>

- [1. Tổng quan](#1-tổng-quan)
- [2. Quản lý proxy](#2-quản-lý-proxy)
  - [2.1 Start, stop, restart](#21-start-stop-restart)
  - [2.2 Khởi động thủ công](#22-khởi-động-thủ-công)
  - [2.2 Running control](#22-running-control)
  - [2.3 Process user](#23-process-user)
- [3. Các loại quy trình proxy](#3-các-loại-quy-trình-proxy)
- [4. Nền tảng được hỗ trợ](#4-nền-tảng-được-hỗ-trợ)
- [5. Ngôn ngữ](#5-ngôn-ngữ)
- [Tài liệu tham khảo](#tài-liệu-tham-khảo)

# 1. Tổng quan
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

# 2. Quản lý proxy

## 2.1 Start, stop, restart

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

## 2.2 Khởi động thủ công
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

## 2.2 Running control
Tùy chọn kiểm soát thời gian chạy:

Option|	Mô tả	|
|---|---|
config_cache_reload|Tải lại bộ đệm cấu hình. 	
Diaginfo [= < target >]|	Thu thập thông tin chẩn đoán trong tệp nhật ký proxy.
snmp_cache_reload	|Tải lại bộ đệm SNMP, xóa các thuộc tính SNMP (thời gian động cơ, khởi động động cơ, id động cơ, thông tin đăng nhập) cho tất cả các máy chủ.	
housekeeper_execute|	Bắt đầu thủ tục dọn phòng.
log_level_increase [= < target >]	|Tăng mức độ nhật ký, ảnh hưởng đến tất cả các quá trình nếu mục tiêu không được chỉ định.
log_level_decrease [= < target >]|	Giảm cấp độ nhật ký, ảnh hưởng đến tất cả các quá trình nếu mục tiêu không được chỉ định.|

Ví dụ:
- Tải lại bộ đệm ẩn cấu hình proxy:
```
shell> zabbix_proxy -c /usr/local/etc/zabbix_proxy.conf -R config_cache_reload
```
- Thu thập thông tin chẩn đoán:

Gather all available diagnostic information in the proxy log file:
```
shell> zabbix_proxy -R diaginfo
Gather history cache statistics in the proxy log file:
shell> zabbix_proxy -R diaginfo=historycache
```
- Tải lại bộ đệm SNMP:
```
shell> zabbix_proxy -R snmp_cache_reload 
```
- Kích hoạt việc thực thi quản gia
```
shell> zabbix_proxy -c /usr/local/etc/zabbix_proxy.conf -R housekeeper_execute
```
- Thay đổi cấp độ nhật ký:

Increase log level of all processes:
```
shell> zabbix_proxy -c /usr/local/etc/zabbix_proxy.conf -R log_level_increase
```
Increase log level of second poller process:
```
shell> zabbix_proxy -c /usr/local/etc/zabbix_proxy.conf -R log_level_increase=poller,2
```
Increase log level of process with PID 1234:
```
shell> zabbix_proxy -c /usr/local/etc/zabbix_proxy.conf -R log_level_increase=1234
```
Decrease log level of all http poller processes:
```
shell> zabbix_proxy -c /usr/local/etc/zabbix_proxy.conf -R log_level_decrease="http poller"
```
## 2.3 Process user
- Zabbix proxy được thiết kế để chạy với tư cách `người dùng không thông thường` không phải `root`. 
- Nếu bạn cố gắng chạy nó dưới dạng `root`, nó sẽ chuyển sang người dùng `zabbix`.
- Chỉ có thể chạy proxy với tư cách là `root` nếu bạn sửa đổi tham số `AllowRoot` trong tệp cấu hình proxy.

# 3. Các loại quy trình proxy
- availability manager
- configuration syncer
- data sender
- discoverer
- heartbeat sender
- history poller
- history syncer
- housekeeper
- http poller
- icmp pinger
- ipmi manager
- ipmi poller
- java poller
- odbc poller
- poller
- preprocessing manager
- preprocessing worker
- self-monitoring
- snmp trapper
- task manager
- trapper
- unreachable poller
- vmware collector
- Tệp nhật ký proxy có thể được sử dụng để quan sát các loại quy trình này.

- Có thể giám sát nhiều loại quy trình proxy Zabbix bằng cách sử dụng item nội bộ zabbix [ process, < type>, < mode>, < state>] .

# 4. Nền tảng được hỗ trợ
- Zabbix proxy chạy trên cùng danh sách các nền tảng được hỗ trợ như máy chủ Zabbix.

# 5. Ngôn ngữ
- proxy yêu cầu ngôn ngữ UTF-8

# Tài liệu tham khảo

1. https://www.zabbix.com/documentation/current/en/manual/concepts/proxy
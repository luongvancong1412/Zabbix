<h1> Danh sách các thiết bị zabbix giám sát được </h1>

<h2> Mục lục </h2>

- [1. Network](#1-network)
  - [1.1 Brocade](#11-brocade)
  - [1.2 Cisco](#12-cisco)
  - [1.3 Dell hardware](#13-dell-hardware)
- [2. Server Monitorings](#2-server-monitorings)
- [3. Databases monitoring](#3-databases-monitoring)
  - [3.1 MySQL](#31-mysql)
    - [3.1.1 Sử dụng Agent](#311-sử-dụng-agent)
    - [3.1.2 Sử dụng ODBC](#312-sử-dụng-odbc)
- [3. Cloud monitoring](#3-cloud-monitoring)
- [4. Application monitoring](#4-application-monitoring)
- [5. Services monitoring](#5-services-monitoring)
- [Bổ sung](#bổ-sung)
- [Tài liệu tham khảo](#tài-liệu-tham-khảo)


<h2>Monitor anything:</h2>

![Imgur](https://i.imgur.com/jkJBzZi.png)

# 1. Network
<h3>Giám sát hiệu suất và sự cố có thể có trong mạng:</h3>

|<h4> Hiệu suất mạng </h4>|<h4> Network health </h4>|<h4> Khi cấu hình thay đổi </h4>|
|---|---|---|
|- Sử dụng băng thông mạng<br>- Tỷ lệ mất gói<br>- Tỷ lệ lỗi interface<br>- CPU hoặc Memory cao<br>- Số lượng kết nối tcp cao bất thường vào 1 ngày trong tuần<br>- Aggregate throughput of core routers is low|- Link is down<br>- System status ở trang thái warning/critical<br>- Nhiệt độ thiết bị (Quá cao/thấp)<br>- Nguồn điện (Power supply) ở trạng thái state<br>- Dung lượng ổ đĩa sắp hết<br>- Fan ở trạng thái critical<br>- No SNMP data collection (Không thu thập dữ liệu SNMP)|- Thêm hoặc xoá thiết bị<br>- Module mạng được thêm, xoá hoặc thay thế<br>- Firmware được nâng cấp<br>- Số Serial thiết bị thay đổi<br>- Interface thay đổi chế độ tốc độ thấp hơn (lower speed) hoặc half-duplex mode (bán song công)


<h3>Zabbix hỗ trợ `Template` cho các nhà cung cấp:</h3>

![Imgur](https://i.imgur.com/0psqUab.png)

- Các thiết bị sử dụng giao thức SNMP
- Port: 161
- Sử dụng `Community string` như password để truy cập (`đối với version v2c`)

- Các thông tin cần thiết để giám sát:
  - Địa chỉ IP của thiết bị
  - Mở port 161
  - chuỗi  `community` trên thiết bị
## 1.1 Brocade
<a href="https://imgur.com/HMWtN8j"><img src="https://i.imgur.com/HMWtN8j.png" width=100 align="left" title="source: imgur.com" /></a>

Brocade Communications Systems, Inc. (công ty con của Broadcom Inc.) chuyên về các sản phẩm mạng lưu trữ và dữ liệu, bao gồm routers và network switches cho môi trường Data center, campus và nhà cung cấp dịch vụ, IP và Fibre Channel, Chức năng mạng ảo hóa (Network Functions Virtualization- NFV) , mạng do phần mềm xác định (software-defined networking - SDN), phần mềm quản lý mạng.

- Các Templates có sẵn trên bản 6.0:
  - Brocade FC SNMP
  - Brocade_Foundry Nonstackable SNMP
  - Brocade_Foundry Performance SNMP
  - Brocade_Foundry Stackable SNMP

- Dữ liệu thu thập:
  - Mức sử dụng CPU của hệ thống (%)
  - Trạng thái Fan
  - Vị trí hệ thống (location)
  - Người liên hệ (system contact details)
  - Tên system
  - system description
  - Hardware serial number
  - Firmware version
  - Memory utilization (%)
  - interface: trạng thái hoạt động, loại, tốc độ
  - Power supply status
  - Overall system health status
  - Uptime (thời gian hoạt động)
  - ICMP (ping, loss, response time)
  - Temperature	(Nhiệt độ)

- Cấu hình SNMP trên Brocade, sử dụng lệnh và làm theo mẫu:
```
snmpconfig --set snmpv1
or
snmpconfig --set snmpv2
```
## 1.2 Cisco

<a href="https://imgur.com/yO2Nw6a"><img src="https://i.imgur.com/yO2Nw6a.png" title="source: imgur.com" width=100 align=left /></a>

Cisco Systems, Inc. là một tập đoàn công nghệ đa quốc gia của Mỹ phát triển, sản xuất và bán phần cứng mạng, thiết bị viễn thông cũng như các dịch vụ và sản phẩm công nghệ cao khác.

- Các Templates có sẵn trên bản 6.0:
  - Cisco ASAv SNMP
  - Cisco Catalyst 3750V2-24FS SNMP
  - Cisco Catalyst 3750V2-24PS SNMP
  - Cisco Catalyst 3750V2-24TS SNMP
  - Cisco Catalyst 3750V2-48PS SNMP
  - Cisco Catalyst 3750V2-48TS SNMP
  - Cisco IOS SNMP
- Mẫu chung cho các thiết bị của Cisco: `Cisco IOS SNMP`

- Dữ liệu thu thập:
  - Sử dụng CPU
  - Trạng thái FAN
  - Vị trí hệ thống (Do người cấu hình thiết bị cấu hình)
  - Chi tiết liên hệ hệ thống (có thể là mail, sdt do người cấu hình thiết bị cấu hình)
  - 	Tên hệ thống
  - Hardware model name
  - Hardware serial number
  - Operating system
  - Bộ nhớ đã sử dụng, trống, mức độ sử dụng bộ nhớ %
  - Network interface: Trạng thái hoạt động, loại interface,...
  - Power supply; trạng thái nguồn điện
  - Uptime: thời gian hoạt động
  - ICMP: ping, loss, response time
  - Temperature: nhiệt độ
- SNMP trên switch Cisco, sử dụng lệnh và làm theo mẫu:
```
# Set chuỗi community
snmp-server community <chuỗi community> ro
#Bật snmp
snmp-server enable traps snmp

#Khai báo thông tin về switch (mô tả tuỳ ý về contact, location switch)
snmp-server contact “Thong tin”
snmp-server location “vi tri”

#Khai báo thông tin zabbix server (IP của zabbix server, public là chuỗi SNMP đã khai báo ở trên )
snmp-server host 172.16.4.180 version 2c public udp-port 162
```

## 1.3 Dell hardware

<a href="https://imgur.com/BwUlMvl"><img src="https://i.imgur.com/BwUlMvl.png" title="source: imgur.com" width=100 align=left /></a>

<br>
Dell là công ty công nghệ máy tính phát triển, bán, sửa chữa và hỗ trợ máy tính cũng như các sản phẩm và dịch vụ liên quan.


<br></br>
- Các Templates có sẵn trên bản 6.0:
  - Dell Force S-Series SNMP
  - Dell iDRAC SNMP
  - DELL PowerEdge R720 by HTTP
  - DELL PowerEdge R720 SNMP
  - DELL PowerEdge R740 by HTTP
  - DELL PowerEdge R740 SNMP
  - DELL PowerEdge R820 by HTTP
  - DELL PowerEdge R820 SNMP
  - DELL PowerEdge R840 by HTTP
  - DELL PowerEdge R840 SNMP

- Mẫu dùng chung: DELL PowerEdge R720 SNMP
- Dữ liệu thu thập:
  - Disk arrays (Trạng thái, Model, Trạng thái pin )

- Updating...
# 2. Server Monitorings
Giám sát sự cố và chỉ số hiệu suất máy chủ:
|<h4> Hiệu suất server </h4>|<h4> Tính khả dụng của máy chủ </h4>|<h4> Khi cấu hình thay đổi </h4>|
|---|---|---|
|- Sử dụng CPU/Memory cao<br>- Sử dụng băng thông<br>- Tỷ lệ mất gói<br>- Tỷ lệ lỗi interface<br>- Số lượng kết nối tcp cao bất thường <br>- Aggregate throughput of core routers is low|- Dung lượng Disk sắp hết<br>- System status ở trạng thái  warning/critical<br>- Nhiệt độ thiết bị quá cao/thấp<br>- Power supply, Fan ở trạng thái critical<br>- No SNMP data collection<br>- Network connection is down|- Các thành phần (components) mới thêm/xoá<br>- Thêm, xoá hoặc thay thế Network module<br>- Firmware được nâng cấp<br>- Số serial thiết bị thay đổi<br>- Interface thay đổi chế độ: lower speed hoặc half-duplex


<h3> Danh sách các máy chủ và hệ điều hành có sẵn Template </h3>

![Imgur](https://i.imgur.com/6szozW8.png)

- Các thiết bị sử dụng `Agent` để giám sát
- Port: 10050,10051

- Các thông tin cần thiết để giám sát:
  - Địa chỉ IP của thiết bị
  - Mở port 10050,10051

- Updating...
# 3. Databases monitoring

|<h4>Hiệu suất cơ sở dữ liệu</h4>|<h4>Tính khả dụng của công cụ cơ sở dữ liệu</h4>|<h4>Thay đổi cấu hình</h4>|
|---|---|---|
|- Sử dụng CPU hoặc bộ nhớ cao<br>- Sử dụng băng thông mạng<br>- Tỷ lệ mất gói<br>- Tỷ lệ lỗi giao diện<br>- Số lượng kết nối tcp cao bất thường vào ngày này trong tuần<br>- Thông lượng tổng hợp của các bộ định tuyến lõi thấp|- Dung lượng đĩa trống sắp hết<br>- Trạng thái hệ thống ở trạng thái cảnh báo / quan trọng<br>- Nhiệt độ thiết bị quá cao / quá thấp<br>- Nguồn điện đang ở trạng thái quan trọng<br>- Quạt đang ở trạng thái nguy kịch<br>- Không thu thập dữ liệu SNMP<br>- Kết nối mạng bị ngắt|- Các thành phần mới được thêm vào hoặc loại bỏ<br>- Mô-đun mạng được thêm, xóa hoặc thay thế<br>- Phần mềm cơ sở đã được nâng cấp<br>- Số sê-ri thiết bị đã thay đổi<br>- Giao diện đã thay đổi thành tốc độ thấp hơn hoặc chế độ bán song công


![Imgur](https://i.imgur.com/74R2Iah.png)

## 3.1 MySQL
- Có sẵn Template trên:
  - MySQL, verion 5.7, 8.0
  - Percona, verion 8.0
  - MariaDB, version 10.4
### 3.1.1 Sử dụng Agent


<h4>Cài đặt:</h4>

1. Cài đặt Agent trên MySQL client
2. Sao chép `template_db_mysql.conf` vào thư mục có cấu hình Agent (`/etc/zabbix/zabbix_agentd.d/`). Khởi động lại Agent
3. Tạo user MySQL để theo dõi
```
CREATE USER 'zbx_monitor'@'%' IDENTIFIED BY '<password>';
GRANT REPLICATION CLIENT,PROCESS,SHOW DATABASES,SHOW VIEW ON *.* TO 'zbx_monitor'@'%';
```
4. Tạo `.my.cnf` trong thư mục home của Agent (`/var/lib/zabbix` đối với Linux và `c:\` đối với Windows) Với nội dung sau:
```
[client]
user='zbx_monitor'
password='<password>'
```
 - Note: user và password trùng với user vừa tạo ở bước 3.
 - Khởi động lại Agent

- Updating...
### 3.1.2 Sử dụng ODBC
- Updating...
# 3. Cloud monitoring
- Updating...
# 4. Application monitoring
- Updating...
# 5. Services monitoring
- Updating...

# Bổ sung
- Lệnh kiểm tra kết nối SNMP trên server Zabbix
- Trên Centos:
```
yum install net-snmp net-snmp-utils -y
snmpwalk -v2c -c public 172.16.10.3
```
- Trên Ubuntu:
```
apt-get install snmp
```
- Updating...
# Tài liệu tham khảo
1. https://www.zabbix.com/solutions
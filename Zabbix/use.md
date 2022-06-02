<h1> Sử dụng Zabbix để ... </h1>

<h2> Mục lục </h2>

- [1. Network monitoring](#1-network-monitoring)
  - [1.1 Brocade](#11-brocade)
  - [1.2 Cisco](#12-cisco)
  - [1.3 Monitoring Dell iDRAC](#13-monitoring-dell-idrac)
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


Monitor anything
- Network monitoring
- Server monitoring
- Cloud monitoring
- Application monitoring
- Services monitoring

# 1. Network monitoring
Giám sát hiệu suất và sự cố có thể có trong mạng:
<h4> Hiệu suất mạng </h4>

  - Sử dụng băng thông mạng
  - Tỷ lệ mất gói
  - Tỷ lệ lỗi interface
  - CPU hoặc Memory cao
  - Số lượng kết nối tcp cao bất thường vào 1 ngày trong tuần
  - Aggregate throughput of core routers is low
<h4> Network health </h4>

- Link is down
- System status ở trang thái warning/critical
- Nhiệt độ thiết bị (Quá cao/thấp)
- Nguồn điện (Power supply) ở trạng thái state
- Dung lượng ổ đĩa sắp hết
- Fan ở trạng thái critical
- No SNMP data collection (Không thu thập dữ liệu SNMP)

<h4> Khi cấu hình thay đổi </h4>

- Thêm hoặc xoá thiết bị
- Module mạng được thêm, xoá hoặc thay thế
- Firmware được nâng cấp
- Số Serial thiết bị thay đổi
- Interface thay đổi chế độ tốc độ thấp hơn (lower speed) hoặc half-duplex mode (bán song công)


Zabbix hỗ trợ `Template` cho các nhà cung cấp:
![Imgur](https://i.imgur.com/0psqUab.png)

- Bảng chi tiết:

STT|Hãng| Support to|Port|Request|
|:---:|:---:|:---:|---|---|
1|Brocade|SNMP|161,162|- IP Address <br>- Community string|
2|Cisco|SNMP|161,162|- IP Address <br>- Community string 
3|Dell|HTTP, SNMP|161,162|- IP Address <br>- Community string
4|D-Link|SNMP|161,162|- IP Address <br>- Community string
5| Netgear|SNMP|161,162|- IP Address <br>- Community string
6| Intel|IPMI|623|
7|Juniper|SNMP|161,162|- IP Address <br>- Community string
8|TP-Link|SNMP|161,162|- IP Address <br>- Community string
9| QTech|SNMP|161,162|- IP Address <br>- Community string
10| Extreme|SNMP|161,162|- IP Address <br>- Community string
11|Alcatel Lucent|SNMP|161,162|- IP Address <br>- Community string
12|Mikrotik|SNMP|161,162|- IP Address <br>- Community string
13|Ubiquiti|SNMP|161,162|- IP Address <br>- Community string

## 1.1 Brocade
- Dữ liệu thu thập:
```
CPU utilization
Firmware version
Hardware serial number
ICMP loss
ICMP ping
ICMP response time
Memory utilization
Overall system health status
SNMP agent availability
SNMP traps (fallback)		
System contact details		
System description		
System location		
System name
System object ID		
Uptime
```
- Cấu hình SNMP trên Brocade, sử dụng lệnh và làm theo mẫu:
```
snmpconfig --set snmpv1
or
snmpconfig --set snmpv2
```
## 1.2 Cisco
- Dữ liệu thu thập: (Templates default: Cisco IOS SNMP)
```
Hardware model name		
Hardware serial number
ICMP loss
ICMP ping
ICMP response time
Operating system
SNMP agent availability
SNMP traps (fallback)		
System contact details		
System description		
System location		
System name
System object ID		
Uptime
```
- Cấu hình SNMP trên switch Cisco, sử dụng lệnh và làm theo mẫu:
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
## 1.3 Monitoring Dell iDRAC
# 2. Server Monitorings
Giám sát sự cố và chỉ số hiệu suất máy chủ:
<h4> Hiệu suất server </h4>

- Sử dụng CPU/Memory cao
- Sử dụng băng thông
- Tỷ lệ mất gói
- Tỷ lệ lỗi interface
- Số lượng kết nối tcp cao bất thường
- Aggregate throughput of core routers is low

<h4> Tính khả dụng của máy chủ </h4>

- Dung lượng Disk sắp hết
- System status ở trạng thái  warning/critical
- Nhiệt độ thiết bị quá cao/thấp
- Power supply, Fan ở trạng thái critical
- No SNMP data collection
- Network connection is down

<h4> Khi cấu hình thay đổi </h4>

- Các thành phần (components) mới thêm/xoá
- Thêm, xoá hoặc thay thế Network module
- Firmware được nâng cấp
- Số serial thiết bị thay đổi
- Interface thay đổi chế độ: lower speed hoặc half-duplex

<h3> Danh sách các máy chủ và hệ điều hành có sẵn Template </h3>

![Imgur](https://i.imgur.com/6szozW8.png)

| use|Port default|Request|
|:---:|:---:|---|
|Agent|10050,10051|- IP Address <br>- Port|

# 3. Databases monitoring

<h4>Hiệu suất cơ sở dữ liệu</h4>

- Sử dụng CPU hoặc bộ nhớ cao
- Sử dụng băng thông mạng
- Tỷ lệ mất gói
- Tỷ lệ lỗi giao diện
- Số lượng kết nối tcp cao bất thường vào ngày này trong tuần
- Thông lượng tổng hợp của các bộ định tuyến lõi thấp

<h4>Tính khả dụng của công cụ cơ sở dữ liệu</h4>

- Dung lượng đĩa trống sắp hết
- Trạng thái hệ thống ở trạng thái cảnh báo / quan trọng
- Nhiệt độ thiết bị quá cao / quá thấp
- Nguồn điện đang ở trạng thái quan trọng
- Quạt đang ở trạng thái nguy kịch
- Không thu thập dữ liệu SNMP
- Kết nối mạng bị ngắt

<h4>Thay đổi cấu hình</h4>

- Các thành phần mới được thêm vào hoặc loại bỏ
- Mô-đun mạng được thêm, xóa hoặc thay thế
- Phần mềm cơ sở đã được nâng cấp
- Số sê-ri thiết bị đã thay đổi
- Giao diện đã thay đổi thành tốc độ thấp hơn hoặc chế độ bán song công

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

### 3.1.2 Sử dụng ODBC

# 3. Cloud monitoring
# 4. Application monitoring
# 5. Services monitoring

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

|Hardware||
|---|---|
CPU| AMD RyzenTM V1500B quad-core 2.2 GHz
Hardware encryption engine| Yes (AES-NI)
Memory |4 GB DDR4 ECC SODIMM (expandable up to 32 GB)
Compatible drive types|8 x 3.5" or 2.5" SATA HDD/SSD (drives not included)
Hot swappable drives |Yes
External ports |• 2 x USB 3.2 Gen 1 ports<br>• 1 x Expansion port (eSATA)
Form factor |Rackmount 2U
Size (HxWxD) |• RS1221+: 88 x 482 x 306.6 mm (with server handles)<br>• RS1221RP+: 88 x 482 x 407.5 mm (with server handles)
Weight |• RS1221+: 6.9 kg<br>• RS1221RP+: 8.4 kg
Rack installation support |• RS1221+: 2-post 19" rack (direct mounting), 4-post 19" rack<br>• RS1221RP+: 4-post 19" rack
LAN ports |4 x 1GbE RJ-45
Wake on LAN/WAN |Yes
PCIe 3.0 slots |• 1 x 4-lane x8 slot<br>• Supports 10GbE/25GbE network interface cards2 and M.2 NVMe SSD adapter cards for SSD cache8
Scheduled power on/off| Yes
System fans| 2 x (80 x 80 x 25 mm)
AC input power voltage| 100 V to 240 V AC
Power consumption| • RS1221+: 49.98 W (Access), 22.64 W (HDD Hibernation)<br>• RS1221RP+: 61.94 W (Access), 29.98 W (HDD Hibernation)
Power frequency| 50/60 Hz, single phase
Operating temperature| 0°C to 35°C (32°F to 95°F)
Storage temperature| -20°C to 60°C (-5°F to 140°F)
Relative humidity| 5% to 95% RH 
Maximum operating altitude| 5,000 m (16,400 ft)
General DSM Specification|
Networking protocols| SMB, AFP, NFS, FTP, WebDAV, CalDAV, iSCSI, Telnet, SSH, SNMP, VPN (PPTP, OpenVPN™, L2TP)
File systems| • Internal: Btrfs, ext4<br>• External: Btrfs, ext4, ext3, FAT32, NTFS, HFS+, exFAT9
Supported RAID types |Synology Hybrid RAID (SHR), Basic, JBOD, RAID 0, RAID 1, RAID 5, RAID 6, RAID 10
Storage management|<br>• Maximum single volume size: 108 TB<br>• Maximum system snapshots: 65,53610<br>• Maximum internal volumes: 64
SSD cache|<br>• Read/write cache support<br>• 2.5" SATA SSD support<br>• M.2 NVMe SSD support8
File sharing capabilities|<br>• Maximum local user accounts: 2,048<br>• Maximum local groups: 256<br>• Maximum shared folders: 512<br>• Maximum concurrent SMB/NFS/AFP/FTP connections: 1,00011
Privileges| Windows® Access Control List (ACL), application privileges
Directory services| Connects with Windows® AD/LDAP servers enabling domain users to login via SMB/NFS/AFP/FTP/File Station using their existing credentials.
Virtualization| VMware vSphere® 6.5, Microsoft Hyper-V®, Citrix®, OpenStack®
Security| Firewall, shared folder encryption, SMB encryption, FTP over SSL/TLS, SFTP, rsync over SSH, login auto block, Let's Encrypt support, HTTPS (customizable cipher suite)
Supported clients| Windows® 7 onwards, macOS® 10.12 onwards
Supported browsers| Chrome®, Firefox®, Edge®, Internet Explorer® 10 onwards, Safari® 10 onwards, Safari (iOS 10 onwards), Chrome (Android™ 6.0 onwards) on tablets




# Tài liệu tham khảo
1. 
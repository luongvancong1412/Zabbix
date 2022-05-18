<h1> Giám sát Linux sử dụng SNMP </h1>

<h2> Mục lục </h2>

- [I. Cài đặt SNMP](#i-cài-đặt-snmp)
  - [1. Trên Ubuntu](#1-trên-ubuntu)
  - [2. Trên Centos 7](#2-trên-centos-7)
- [II. Thêm host trên Zabbix frontend:](#ii-thêm-host-trên-zabbix-frontend)
  - [1. Kiểm tra trên Zabbix server](#1-kiểm-tra-trên-zabbix-server)
  - [2. Thêm host trên zabbix frontend](#2-thêm-host-trên-zabbix-frontend)
- [Tài liệu tham khảo](#tài-liệu-tham-khảo)


# I. Cài đặt SNMP
## 1. Trên Ubuntu

- Cài đặt SNMP:
```
sudo apt -y install snmpd
```

- Khởi động và cấu hình khởi động cùng hệ thống:
```
sudo systemctl start snmpd
sudo systemctl enable snmpd
```

- Backup file cấu hình:
```
sudo cp /etc/snmp/snmpd.conf /etc/snmp/snmpd.conf.bak
```
- Sửa cấu hình:
```
sudo sed -i 's/agentAddress  udp:127.0.0.1:161/agentAddress udp:161,udp6:[::1]:161/g' /etc/snmp/snmpd.conf
```

- Khởi động lại dịch vụ:
```
sudo systemctl restart snmpd
```
## 2. Trên Centos 7
- Updating ...
# II. Thêm host trên Zabbix frontend:
## 1. Kiểm tra trên Zabbix server

- Sử dụng câu lệnh:
```
snmpwalk -v2c -c public 192.168.77.135
```
- Thành công chuyển sang bước tiếp theo

![Imgur](https://i.imgur.com/r233Nhs.png)

## 2. Thêm host trên zabbix frontend

- Truy cập: http://ip_server_zabbix/zabbix
  - Ví dụ: http://192.168.77.130/zabbix
- Đăng nhập
- Chọn: `Administritor` > `Hosts`

!![Imgur](https://i.imgur.com/4Add1Sn.png)

- Chọn `Create host` trên góc bên phải
- Nhập thông tin:
  - `Host name`: Tên host giám sát
  - `Templates`: Mẫu áp dụng cho host
  - `Groups`: Thêm host vào nhóm
  - `Interface`: chọn SNMP và nhập địa chỉ IP host

![Imgur](https://i.imgur.com/ZyRrGzC.png)

- Sang Tab `Macros`:
  - Nhập thông tin `rocommunity` mặc định là `public`

![Imgur](https://i.imgur.com/lI4LEcE.png)

- Chọn `Add` để thêm
- Trạng thái trường `Availability` chuyển sang xanh là OK

![Imgur](https://i.imgur.com/IDY6Zdh.png)

# Tài liệu tham khảo
1. https://www.zabbix.com/documentation/current/it/manual/config/items/itemtypes/snmp
2. 
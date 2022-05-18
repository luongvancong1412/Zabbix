<h1> Giám sát Linux sử dụng SNMP </h1>

<h2> Mục lục </h2>

- [I. Cài đặt SNMP](#i-cài-đặt-snmp)
  - [1. Trên Ubuntu](#1-trên-ubuntu)
- [II. Thêm host trên Zabbix frontend:](#ii-thêm-host-trên-zabbix-frontend)
  - [1. Kiểm tra trên Zabbix server](#1-kiểm-tra-trên-zabbix-server)
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
sudo systemctl enabled snmpd
```

- Backup file cấu hình:
```
cp /etc/snmp/snmpd.conf /etc/snmp/snmpd.conf.bak
```
- Sửa cấu hình:
```
sed -i 's/agentAddress  udp:127.0.0.1:161/agentAddress udp:161,udp6:[::1]:161/g' /etc/snmp/snmpd.conf
```
    Hoặc
```
sed -i 's/agentAddress  udp:127.0.0.1:161/agentAddress udp:192.168.77.130:161/g' /etc/snmp/snmpd.conf
```

- Thêm dòng vào cuối file:
```
echo 'rocommunity Conglv' >> /etc/snmp/snmpd.conf
```
- Khởi động lại dịch vụ:
```
sudo systemctl restart snmpd
```
# II. Thêm host trên Zabbix frontend:
## 1. Kiểm tra trên Zabbix server

- Sử dụng câu lệnh:
```
snmpwalk -v2c -c Conglv 192.168.77.135
```
-
# Tài liệu tham khảo
1. https://www.zabbix.com/documentation/current/it/manual/config/items/itemtypes/snmp
2. 
<h1> Giám sát router Mikrotik </h1>

<h2> Mục lục </h2>

- [1. Mô hình](#1-mô-hình)
- [2. Cấu hình router Mikrotik](#2-cấu-hình-router-mikrotik)
  - [2.1 Cấu hình SNMP](#21-cấu-hình-snmp)
  - [2.2 Cấu hình Zabbix](#22-cấu-hình-zabbix)
    - [2.2.1 Kiểm tra kết nối](#221-kiểm-tra-kết-nối)
    - [2.2.2 Thêm host vào Zabbix qua frontend](#222-thêm-host-vào-zabbix-qua-frontend)
- [Tài liệu tham khảo](#tài-liệu-tham-khảo)
# 1. Mô hình
![Imgur](https://i.imgur.com/JlRqqqz.png)
# 2. Cấu hình router Mikrotik
- `SNMP` là viết tắt của cụm từ `Simple Network Management Protocol`. 
- Là giao thức được sử dụng rất phổ biến để giám sát và điều khiển thiết bị mạng như switch, router, server ...

- Cơ chế bảo mật: `Community String`
  - là một chuỗi ký tự được cài đặt giống nhau trên cả SNMP manager và router
  - Đóng vai trò như `Password` giữa 2 bên khi trao đổi dữ liệu

- Các phiên bản SNMP:
  - SNMPv1
  - SNMPv2
  - SNMPv2c
  - SNPv2u
  - SNMPv3

- Để giám sát Router qua SNMP cần:
  - `Bật dịch vụ SNMP` trên Router
  - Địa chỉ `IP Router`
  - Chuỗi `Community`
## 2.1 Cấu hình SNMP
- Kết nối với Router Mikrotik (Winbox, telnet, ssh,...)
- Bật dịch vụ SNMP:
```
snmp set enabled=yes
```
- Xem `community` đã có sẵn trên MikroTik router
```
snmp community print
```
- Mặc định MikroTik có một community là `public`, có số ID là `0`

```
[admin@MikroTik] > snmp community print 
Flags: * - default, X - disabled 
 #    NAME    ADDRESSES                                      SECURITY   READ-ACCESS WRITE-ACCESS
 0 *  public  ::/0                                           none       yes         no 
```

- Đổi tên Community:
```
snmp community set name=Conglv 0
```
- Hoặc thêm community:
```
snmp community add name=Test
```

- Kiểm tra lại:
```
[admin@MikroTik] > snmp community print
Flags: * - default, X - disabled 
 #    NAME  ADDRESSES                                        SECURITY   REA WRI
 0 *  pub.. ::/0                                             none       yes no 
 1    Test  ::/0                                             none       yes no
```

- (Option) có thể đặt địa chỉ liên hệ và vị trí SNMP:
```
snmp set contact="Luong Van Cong <conglv7198@gmail.com>"
snmp set location="100TK-TT-HN"
```

- Xem tóm tắt cấu hình SNMP đã cài:
```
[admin@MikroTik] > snmp print 
          enabled: yes
          contact: Luong Van Cong <conglv7198@gmail.com>
         location: 100TK-TT-HN
        engine-id: 
      trap-target: 
   trap-community: Conglv
     trap-version: 1
  trap-generators: temp-exception
```

## 2.2 Cấu hình Zabbix
### 2.2.1 Kiểm tra kết nối
- Trên Zabbix server, cài đặt và kiểm tra kết nối SNMP:
```
sudo apt-get install snmp
snmpwalk -v2c - Conglv 192.168.77.133
```

Trong đó: 
- `192.168.77.133` là địa chỉ IP của MikroTik router.
- `Conglv` : Password giao tiếp giữa Zabbix server và router MikroTik

![Imgur](https://i.imgur.com/bQnUVkm.png)

### 2.2.2 Thêm host vào Zabbix qua frontend

- Đăng nhập vào giao diện quản trị Zabbix:
  - Ở đây là : `http://192.168.77.130`
- Chọn: `Configuration` > `Hosts` > `Create host`
- Nhập thông tin của host:

![Imgur](https://i.imgur.com/IXb3FQ1.png)

- Chọn `Add` để thêm host

- Thêm host `thành công` khi trạng thái chuyển từ ![Imgur](https://i.imgur.com/M7CW0QY.png) thành ![Imgur](https://i.imgur.com/jJgAjyR.png).

# Tài liệu tham khảo

1. https://techexpert.tips/zabbix/monitor-mikrotik-zabbix/
<h1> Cài đặt Agent trên Windows Server</h1>

<h2> Mục lục </h2>

- [1. Mô hình mạng](#1-mô-hình-mạng)
- [2. Cài đặt Agent trên Windows Server](#2-cài-đặt-agent-trên-windows-server)
- [3. Thêm Windows Server trên Zabbix](#3-thêm-windows-server-trên-zabbix)
- [Tài liệu tham khảo](#tài-liệu-tham-khảo)

# 1. Mô hình mạng
# 2. Cài đặt Agent trên Windows Server

- Chọn phiên bản `Agent` cho `Window Server`: [tại đây](https://www.zabbix.com/download_agents?version=6.0+LTS&release=6.0.4&os=Windows&os_version=Any&hardware=amd64&encryption=OpenSSL&packaging=MSI&show_legacy=0).

![Imgur](https://i.imgur.com/GMtrTio.png)

- Tải về `Window Server`:

![Imgur](https://i.imgur.com/kZWH4Ab.png)

- Chọn `Install` để cài đặt (Quá trình cài đặt không cần sử dụng mạng)

![Imgur](https://i.imgur.com/WolFs38.png)

- Chọn `Next`

![Imgur](https://i.imgur.com/xuejYpX.png)
- Chọn `I accept the terms in the License Agreement`. Sau đó chọn `Next`

![Imgur](https://i.imgur.com/lKlN83b.png)

- Nhập thông tin cấu hình Zabbix Agent: `Host name`, `IP Zabbix server`, `listen port`.

![Imgur](https://i.imgur.com/9ApoAYR.png)
- Có thể chọn nơi lưu trữ Agent. Để mặc định, chọn `Next`

![Imgur](https://i.imgur.com/4IbPOJL.png)

- Chọn `Install` để bắt đầu quá trình cài đặt

![Imgur](https://i.imgur.com/P1tXFrt.png)

- Chọn `Finish` để hoàn tất quá trình cài đặt

![Imgur](https://i.imgur.com/MRA2KiL.png)

# 3. Thêm Windows Server trên Zabbix
- Truy cập Zabbix Frontend:http://ip_server_zabbix/zabbix
Trong bài này: http://192.168.77.130/zabbix

- Chọn `Configuration` → `Hosts` → `Create host`
![Imgur](https://i.imgur.com/w8hNIfS.png)

- Nhập thông tin host: `Host name`, `Templates`, `Groups`, `Interface`. Những trường khác có thể để theo mặc đinh. Chọn `Add` để thêm.

![Imgur](https://i.imgur.com/SbwyDjY.png)

- Trạng thái `ZBX` chuyển thành màu xanh lá, quá trình cài đặt hoàn tất
 
![Imgur](https://i.imgur.com/F0wHPJ6.png)

# Tài liệu tham khảo
1. https://www.zabbix.com/documentation/current/en/manual
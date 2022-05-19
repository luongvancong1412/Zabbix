<h1> Zabbix </h1>

<img src=https://i.imgur.com/3zAIpt7.png width=50% align="right">

- `Zabbix` là một phần mềm `mã nguồn mở` `giám sát các mạng và ứng dụng`, được phát hành lần đầu tiên vào năm `2001` bởi `Alexei Vladishev`. 
- Nó được thiết kế để giúp quản trị viên mạng `giám sát và theo dõi tình trạng` của các dịch vụ mạng, server và phần cứng mạng khác nhằm đảm bảo hệ thống luôn luôn được ổn định.

<h2>Summary</h2>

[I. Network Monitor](Network-Monitor/Network-monitor.md)

- [1. Giám sát mạng là gì](Network-Monitor/Network-monitor.md#1-giám-sát-mạng-là-gì)
- [2. Các loại giám sát](Network-Monitor/Network-monitor.md#2-các-loại-giám-sát)
- [3. Thông tin thêm](Network-Monitor/Network-monitor.md#3-thông-tin-thêm)

[II. Zabbix](Zabbix)

- [1. Tổng quan về Zabbix](Zabbix/Overview/Info.md)
  - [1.1. Zabbix là gì?](Zabbix/Overview/Info.md#1-zabbix-là-gì)
  - [1.2. Lịch sử phát triển và các phiên bản](Zabbix/Overview/Info.md#2-lịch-sử-phát-triển-và-các-phiên-bản)
  - [1.3. Các tính năng](Zabbix/Overview/Info.md#3-các-tính-năng-của-zabbix)
  - [1.4. Architecture](Zabbix/Overview/Info.md#4-architecture)
  - [1.5. Ưu điểm](Zabbix/Overview/Info.md#5-ưu-điểm-của-zabbix)
  - [1.6. Những cải thiện](Zabbix/Overview/Info.md#6-những-điều-cải-thiện)
- [2. Thuật ngữ thường được sử dụng](Zabbix/Thuat-ngu.md)
- [3. Zabbix processes](Zabbix/processes)
  - [3.1 Server](Zabbix/processes/server.md)
  - [3.2 Agent](Zabbix/processes/agent.md)
  - [3.3 Agent 2](Zabbix/processes/agent2.md)
  - [3.4 Proxy](Zabbix/processes/proxy.md)
  - Updating...
- [4. Cài đặt](Zabbix/install)
  - [4.1 Cài đặt Zabbix trên Ubuntu 20.04](Zabbix/install/1-Server-Ubuntu20.04.md)
  - [4.2 Cài đặt Agent trên Ubuntu 18.04](Zabbix/install/2-Agent-Ubuntu18.04.md)
  - [4.3 Cài đặt Agent trên Centos 7](Zabbix/install/3-Agent-Centos7.md)
  - [4.4 Cài đặt Agent trên Windows Server](Zabbix/install/4-Agent-WinSRV2012.md)
  - Updating...
- [5. Quickstart](Zabbix/Quickstart)
  - [5.1 Login và Quản lý user](Zabbix/Quickstart/1-Login&User.md)
  - [5.2 New hosts](Zabbix/Quickstart/2-New-host.md)
  - [5.3 New item](Zabbix/Quickstart/3-New-item.md)
  - [5.4 New trigger](Zabbix/Quickstart/4-New-trigger.md)
  - [5.5 Nhận báo cáo sự cố](Zabbix/Quickstart/5-Receiving-Problem-notification.md)
    - [Telegram](Zabbix/Configuration/10-Alert-Telegram.md#i-telegram-webhook)
    - [Gmail](Zabbix/Configuration/10-Alert-Telegram.md#ii-gmail)
  - [5.6 New template](Zabbix/Quickstart/6-New-template.md)
  - Updating...

- [6. Configuration]()
  - [6.1 Host và host group](Zabbix/Configuration/1-Host&host-groups.md)
  - [6.2 Items](Zabbix/Configuration/2-Items.md)
  - [6.3 Triggers](Zabbix/Configuration/3-Triggers.md)
  - [6.4 Events](Zabbix/Configuration/4-Events.md)
  - [6.5 Macros](Zabbix/Configuration/8-Macros.md)
  - [6.6 Templates](Zabbix/Configuration/9-Templates.md)
  - [6.7 Visualization](Zabbix/Configuration/7-Visualization.md)
  - Updating...

- [7. Service monitoring](Zabbix/Service-monitoring)
- [8. Biểu thức chính quy](Zabbix/bieu-thuc-chinh-quy.md)
- [9. Agentless](Zabbix/Agentless/)
  - [9.1 Giám sát Linux sử dụng SNMP](Zabbix/Agentless/1-Monitor-Linux-SNMP.md)
  - [9.2 Giám sát Router MikroTik](Zabbix/Agentless/2-Monitor-Mikrotik.md)
- Updating...

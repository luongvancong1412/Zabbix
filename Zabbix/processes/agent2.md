<h1> Agent 2</h2>

<h2> Mục lục </h2>

- [1. Tổng quan](#1-tổng-quan)
  - [1.1 Kiểm tra đồng thời](#11-kiểm-tra-đồng-thời)
- [2. Nền tảng được hỗ trợ](#2-nền-tảng-được-hỗ-trợ)
- [3. Cài đặt](#3-cài-đặt)
- [Tài liệu tham khảo](#tài-liệu-tham-khảo)

# 1. Tổng quan
- Zabbix agent 2 là một thế hệ mới của Zabbix agent
- Có thể được sử dụng thay cho Zabbix agent

- Mục đích phát triển Agent 2:
  - Giảm số lượng kết nối TCP
  - Cung cấp cải tiến của checks
  - Có thể dễ dàng mở rộng với các plugin (công cụ). Một plugin sẽ có thể:
    - Cung cấp các check nhỏ chỉ bằng một vài dòng code đơn giản
    - Cung cấp các check phức tạp bao gồm các long-running script và thu thập dữ liệu độc lập với việc gửi lại dữ liệu định kỳ
  - Thay thế cho Zabbix agent (trong đó nó hỗ trợ tất cả các chức năng trước đó)

- Agent 2 được viết bằng Go (với một số code C của Agent Zabbix được sử dụng lại).
- Agent 2 không có hỗ trợ daemonization tích hợp trên Linux; nó có thể được chạy như một dịch vụ Windows .

- Check Passive hoạt động tương tự như Zabbix agent. 
- Check Active hỗ trợ các khoảng thời gian được lập lịch/ linh hoạt và kiểm tra đồng thời trong một sever đang hoạt động.

## 1.1 Kiểm tra đồng thời

- Check từ các plugin khác nhau có thể được thực hiện đồng thời. Số lần check đồng thời trong một plugin bị giới hạn bởi cài đặt dung lượng plugin. Mỗi plugin có thể có cài đặt dung lượng mã cứng (100 là mặc định) có thể được giảm xuống bằng cách sử dụng Plugins.`<PluginName>.System.Capacity=N` cài đặt trong thông số cấu hình Plugin . Tên cũ của thông số này vẫn được hỗ trợ, nhưng đã không được chấp nhận trong Zabbix 6.0.

# 2. Nền tảng được hỗ trợ
Agent 2 được hỗ trợ cho nền tảng Linux và Windows.

Nếu cài đặt từ các gói, Agent 2 được hỗ trợ trên:

- RHEL/CentOS 6, 7, 8
- SLES 15 SP1 +
- Debian 9, 10
- Ubuntu 18.04, 20.04
Trên Windows Agent 2 được hỗ trợ trên:

- Windows Server 2008 R2 trở lên
- Windows 7 trở lên
# 3. Cài đặt
- Zabbix agent 2 có sẵn trong các gói Zabbix.
- Để biên dịch Zabbix agent 2 từ các nguồn, phải chỉ định option cấu hình  `--enable-agent2`.

# Tài liệu tham khảo

1. https://www.zabbix.com/documentation/current/en/manual/concepts/agent2
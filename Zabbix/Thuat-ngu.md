<h1>Thuật ngữ</h1>

- [Host](#host)
- [Host group](#host-group)
- [Item](#item)
- [Value preprocessing](#value-preprocessing)
- [Trigger](#trigger)
- [Event](#event)
- [Event tag](#event-tag)
- [Event correlation](#event-correlation)
- [Problem](#problem)
- [Problem update](#problem-update)
- [Action](#action)
- [Escalation](#escalation)
- [Media](#media)
- [Notification](#notification)
- [Remote command](#remote-command)
- [Template](#template)
- [Web scenario](#web-scenario)
- [frontend](#frontend)
- [Dashboard](#dashboard)
- [Widget](#widget)
- [Zabbix API](#zabbix-api)
- [Zabbix server](#zabbix-server)
- [Zabbix proxy](#zabbix-proxy)
- [Zabbix agent](#zabbix-agent)
- [Zabbix agent 2](#zabbix-agent-2)
- [Encryption](#encryption)
- [Network discovery](#network-discovery)
- [Low-level discovery](#low-level-discovery)
- [Low-level discovery rule](#low-level-discovery-rule)
- [Item prototype](#item-prototype)
- [Trigger prototype](#trigger-prototype)
- [Agent autoregistration](#agent-autoregistration)
- [Tài liệu tham khảo](#tài-liệu-tham-khảo)

Một số thuật ngữ thường được sử dụng trong Zabbix

# Host

- Một thiết bị được nối mạng cần giám sát, cài sẵn IP, DNS
(*a networked device that you want to monitor, with IP/DNS.*)

# Host group

- Một nhóm logic của các host; chứa các host và mẫu. host vào mẫu không được liên kết với nhau theo bất kỳ cách nào.
- Sử dụng nhóm host khi cần gán quyền truy cập vào host cho các nhóm người dùng khác nhau.
(*a logical grouping of hosts; it may contain hosts and templates. Hosts and templates within a host group are not in any way linked to each other. Host groups are used when assigning access rights to hosts for different user groups.*)

# Item


- Một phần dữ liệu cụ thể mà bạn muốn nhận từ một host lư trữ.
(*a particular piece of data that you want to receive off of a host, a metric of data.*)

# Value preprocessing

- Chuyển đổi giá trị số liệu đã nhận trước khi lưu nó vào cơ sở dữ liệu
(*a transformation of received metric value before saving it to the database.*)

# Trigger

- Một biểu thức logic xác định ngưỡng vấn đề và được sử dụng để "đánh giá" dữ liệu nhận được trong items
(*a logical expression that defines a problem threshold and is used to "evaluate" data received in items.*)

- Khi dữ liệu nhận được vượt quá ngưỡng, triggers sẽ chuyển từ trạng thái "OK" sang "Problem" (Sự cố).  Khi dữ liệu nhận được dưới ngưỡng, triggers trở lại trạng thái 'Ok'
(*When received data are above the threshold, triggers go from 'Ok' into a 'Problem' state. When received data are below the threshold, triggers stay in/return to an 'Ok' state.*)

# Event

- Một lần xuấ hiện duy nhất của điều gì đó đáng được chú ý ví dụ như trigger chuyển trạng thái hoặc  quá trình tự động đăng ký Agent đang diễn ra,...
(*a single occurrence of something that deserves attention such as a trigger changing state or a discovery/agent autoregistration taking place.*)

# Event tag

- Một điểm đánh dấu, dấu hiệu được xác định trước cho event. Nó có thể được sử dụng trong tương quan sự kiện, tạo chi tiết quyền,...
(*a pre-defined marker for the event. It may be used in event correlation, permission granulation, etc.*)

# Event correlation

- Một phương pháp giải quyết vấn đề một cách linh hoạt và chính xác.
(*a method of correlating problems to their resolution flexibly and precisely.*)

- Ví dụ: bạn có thể xác định rằng sự cố được báo cáo bởi một trigger có thể được giải quyết bởi một trigger khác, thậm chí có thể sử dụng một phương pháp thu thập dữ liệu khác.
(*For example, you may define that a problem reported by one trigger may be resolved by another trigger, which may even use a different data collection method.*)

# Problem

- trigger ở trạng thái "Sự cố".
(*a trigger that is in "Problem" state.*)

# Problem update

- Các option quản lý Problem do Zabbix cung cấp ví dụ như thêm nhận xét, xác nhận, thay đổi mức độ nghiêm trọng hoặc đóng theo cách thủ công.
(*problem management options provided by Zabbix, such as adding comment, acknowledging, changing severity or closing manually.*)

# Action

- Một phương pháp được xác định trước để phản ứng với sự kiện.
(*a predefined means of reacting to an event.*)

- Một hành động bao gồm 
  - Các hoạt động (e.g. gửi thông báo)
  - Và các điều kiện ( khi hoạt động được thực hiện)
(*An action consists of operations (e.g. sending a notification) and conditions (when the operation is carried out)*)

# Escalation
-  một kịch bản tùy chỉnh để thực hiện các hoạt động trong một hành động; một chuỗi gửi thông báo/thực hiện lệnh từ xa.
- (*a custom scenario for executing operations within an action; a sequence of sending notifications/executing remote commands.*)

# Media
- Phương tiện gửi thông báo; kênh giao hàng
(*a means of delivering notifications; delivery channel.*)

# Notification

- Một thông báo gửi đến người dùng về 1 sự kiện qua kênh media đã chọn
(*a message about some event sent to a user via the chosen media channel.*)

# Remote command

- Một lệnh viết trước được thực thi tự động trên một host được giám sát.
(*a pre-defined command that is automatically executed on a monitored host upon some condition.*)

# Template

- Một tập hợp các thực thể (items, triggers, đồ thị, quy tắc khám phá cấp thấp, kịch bản web) có thể áp dụng cho 1 hoặc một số host.
(*a set of entities (items, triggers, graphs, low-level discovery rules, web scenarios) ready to be applied to one or several hosts.*)

- Công việc của các template là
  - Tăng tốc độ triển khai các nhiệm vụ giám sát trên host lưu trữ;
  - Giúp việc áp dụng các thay đổi hàng loạt vào các nhiệm vụ giám sát dễ dàng hơn. Các template được liên kết trực tiếp với các host riêng lẻ.
(*The job of templates is to speed up the deployment of monitoring tasks on a host; also to make it easier to apply mass changes to monitoring tasks. Templates are linked directly to individual hosts.*)

# Web scenario

- Là một hoặc 1 số request HTTP để kiểm tra tính khả dụng (availability) của một website.
(*one or several HTTP requests to check the availability of a web site.*)

# frontend
- Là giao diện web được cung cấp bởi Zabbix
(*the web interface provided with Zabbix.*)

# Dashboard
- Bảng điều khiển or trang tổng quan
- là phần có thể tuỳ chỉnh của giao diện web, hiển thị tóm tắt và hình ảnh hoá thông tin quan trọng được gọi là widget
(*customizable section of the web interface displaying summaries and vizualizations of important information in visual units called widgets.*)

# Widget

- Đơn vị hiển thị trực quan thông tin của 1 loại và nguồn ( 1 tóm tắt, 1 bản đồ, 1 đồ thị, ...) nhất định được sử dụng trong dasdboard
- (*visual unit displaying information of a certain kind and source (a summary, a map, a graph, the clock, etc), used in the dashboard.*)

# Zabbix API

- Zabbix API cho phép bạn sử dụng giao thức JSON RPC để tạo, cập nhật và tìm nạp các đối tượng Zabbix (như host, item, đồ thị và các đối tượng khác) hoặc thực hiện bất kỳ tác vụ tùy chỉnh nào khác.
- (*Zabbix API allows you to use the JSON RPC protocol to create, update and fetch Zabbix objects (like hosts, items, graphs and others) or perform any other custom tasks.*)

# Zabbix server
- Một quy trình trung tâm của phần mềm Zabbix thực hiện giám sát, tương tác với các proxy và Agent của Zabbix, tính toán các triggers, gửi thông báo; 
- Một kho dữ liệu trung tâm.
- (*a central process of Zabbix software that performs monitoring, interacts with Zabbix proxies and agents, calculates triggers, sends notifications; a central repository of data.*)

# Zabbix proxy
- Một quy trình có thể thu thập dữ liệu thay mặt cho server Zabbix, làm giảm tải một số quá trình xử lý của server.
- (*a process that may collect data on behalf of Zabbix server, taking some processing load off of the server.*)

# Zabbix agent
- một quy trình được triển khai trên các item tiêu giám sát để chủ động giám sát các tài nguyên và ứng dụng cục bộ của thiết bị đó.
- (*a process deployed on monitoring targets to actively monitor local resources and applications.*)

# Zabbix agent 2

- Agent thế hệ mới, chủ động theo dõi cácc tài nguyên và ứng dụng cục bộ, cho phép sử dụng các plugin để giám sát
- (*a new generation of Zabbix agent to actively monitor local resources and applications, allowing to use custom plugins for monitoring.*)

- Nếu trong tài liệu viết Agent Zabbix thì đó là viết tắt của cả 2 (Agent Zabbix và Agent Zabbix 2) khi chúng hoạt động giống nhau.
- Chỉ viết Agent Zabbix 2 khi chức năng nó khác nhau.

# Encryption
- Mã hoá
- Mã hoá thông tin liên lạc giữa các thành phần Zabbix (server, proxy, Agent, zabbix_sender và zabbix_get) sử dụng giao thức Transport Layer Security (TLS).
- (*support of encrypted communications between Zabbix components (server, proxy, agent, zabbix_sender and zabbix_get utilities) using Transport Layer Security (TLS) protocol.*)

# Network discovery

- Tự động khám phá, tìm kiếm các thiết bị mạng
- (*automated discovery of network devices.*)

# Low-level discovery

- Tự động khám phá, tìm kiếm các thực thể cấp thấp trên một thiết bị cụ thể (ví dụ: file system, network interface, v.v.).
- (*automated discovery of low-level entities on a particular device (e.g. file systems, network interfaces, etc).*)

# Low-level discovery rule

- Tập hợp các định nghĩa để tự động khám phá các thực thể cấp thấp trên một thiết bị.
- (*set of definitions for automated discovery of low-level entities on a device.*)

# Item prototype

- Là  1 biến chỉ với tham số có chỉ số nhất định , sẵn sàng cho việc low-level discovery . Sau khi low-level discovery, các biến sẽ tự động được thay thế bằng các tham số thực được phát hiện và tự động bắt đầu thu thập dữ liệu.
- (*a metric with certain parameters as variables, ready for low-level discovery. After low-level discovery the variables are automatically substituted with the real discovered parameters and the metric automatically starts gathering data.*)

# Trigger prototype
- Là một trigger với các tham số nhất định dưới dạng biến, sẵn sàng cho việc low-level discovery . Sau khi low-level discovery, các biến sẽ tự động được thay thế bằng các tham số thực được phát hiện và trigger tự động bắt đầu đánh giá dữ liệu.
- (*a trigger with certain parameters as variables, ready for low-level discovery. After low-level discovery the variables are automatically substituted with the real discovered parameters and the trigger automatically starts evaluating data.*)

- Nguyên mẫu của một số thực thể Zabbix khác cũng được sử dụng trong low-level discovery - nguyên mẫu biểu đồ, nguyên mẫu host, nguyên mẫu nhóm host.
Prototypes of some other Zabbix entities are also in use in low-level discovery - graph prototypes, host prototypes, host group prototypes.

# Agent autoregistration

- Quy trình Agent Zabbix tự động đăng ký làm host lưu trữ và bắt đầu giám sát.
- (*automated process whereby a Zabbix agent itself is registered as a host and started to monitor.*)

# Tài liệu tham khảo

1. https://www.zabbix.com/documentation/current/en/manual/definitions
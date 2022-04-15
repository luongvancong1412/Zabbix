<h1>Thuật ngữ</h1>

- [Host](#host)
- [Host group](#host-group)
- [Item](#item)
- [Value preprocessing](#value-preprocessing)
- [Trigger](#trigger)
- [Event](#event)
- [Event tag](#event-tag)
- [Event correlation](#event-correlation)

Một số thuật ngữ thường được sử dụng trong Zabbix

# Host

- Một thiết bị được nối mạng cần giám sát, cài sẵn IP, DNS
(*a networked device that you want to monitor, with IP/DNS.*)

# Host group

- Một nhóm logic của các máy chủ; chứa các máy chủ và mẫu. Máy chủ vào mẫu không được liên kết với nhau theo bất kỳ cách nào.
- Sử dụng nhóm máy chủ khi cần gán quyền truy cập vào máy chủ cho các nhóm người dùng khác nhau.
(*a logical grouping of hosts; it may contain hosts and templates. Hosts and templates within a host group are not in any way linked to each other. Host groups are used when assigning access rights to hosts for different user groups.*)

# Item


- Một phần dữ liệu cụ thể mà bạn muốn nhận từ một máy chủ lư trữ.
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

- Một điểm đánh dấu được xác định trước cho event. Nó có thể được sử dụng trong tương quan sự kiện, tạo chi tiết quyền,...
(*a pre-defined marker for the event. It may be used in event correlation, permission granulation, etc.*)

# Event correlation

- a method of correlating problems to their resolution flexibly and precisely.

For example, you may define that a problem reported by one trigger may be resolved by another trigger, which may even use a different data collection method.

problem

- a trigger that is in "Problem" state.

problem update

- problem management options provided by Zabbix, such as adding comment, acknowledging, changing severity or closing manually.

action

- a predefined means of reacting to an event.

An action consists of operations (e.g. sending a notification) and conditions (when the operation is carried out)

escalation

- a custom scenario for executing operations within an action; a sequence of sending notifications/executing remote commands.

media

- a means of delivering notifications; delivery channel.

notification

- a message about some event sent to a user via the chosen media channel.

remote command

- a pre-defined command that is automatically executed on a monitored host upon some condition.

template

- a set of entities (items, triggers, graphs, low-level discovery rules, web scenarios) ready to be applied to one or several hosts.

The job of templates is to speed up the deployment of monitoring tasks on a host; also to make it easier to apply mass changes to monitoring tasks. Templates are linked directly to individual hosts.

web scenario

- one or several HTTP requests to check the availability of a web site.

frontend

- the web interface provided with Zabbix.

dashboard

- customizable section of the web interface displaying summaries and vizualizations of important information in visual units called widgets.

widget

- visual unit displaying information of a certain kind and source (a summary, a map, a graph, the clock, etc), used in the dashboard.

Zabbix API

- Zabbix API allows you to use the JSON RPC protocol to create, update and fetch Zabbix objects (like hosts, items, graphs and others) or perform any other custom tasks.

Zabbix server

- a central process of Zabbix software that performs monitoring, interacts with Zabbix proxies and agents, calculates triggers, sends notifications; a central repository of data.

Zabbix proxy

- a process that may collect data on behalf of Zabbix server, taking some processing load off of the server.

Zabbix agent

- a process deployed on monitoring targets to actively monitor local resources and applications.

Zabbix agent 2

- a new generation of Zabbix agent to actively monitor local resources and applications, allowing to use custom plugins for monitoring.

 Because Zabbix agent 2 shares much functionality with Zabbix agent, the term "Zabbix agent" in documentation stands for both - Zabbix agent and Zabbix agent 2, if the functional behavior is the same. Zabbix agent 2 is only specifically named where its functionality differs.
encryption

- support of encrypted communications between Zabbix components (server, proxy, agent, zabbix_sender and zabbix_get utilities) using Transport Layer Security (TLS) protocol.

network discovery

- automated discovery of network devices.

low-level discovery

- automated discovery of low-level entities on a particular device (e.g. file systems, network interfaces, etc).

low-level discovery rule

- set of definitions for automated discovery of low-level entities on a device.

item prototype

- a metric with certain parameters as variables, ready for low-level discovery. After low-level discovery the variables are automatically substituted with the real discovered parameters and the metric automatically starts gathering data.

trigger prototype

- a trigger with certain parameters as variables, ready for low-level discovery. After low-level discovery the variables are automatically substituted with the real discovered parameters and the trigger automatically starts evaluating data.

Prototypes of some other Zabbix entities are also in use in low-level discovery - graph prototypes, host prototypes, host group prototypes.

agent autoregistration

- automated process whereby a Zabbix agent itself is registered as a host and started to monitor.
<h1> Thay đổi form tin nhắn cảnh báo Telegram/gmail </h1>

<h2> Mục lục </h2>

- [1. Telegram](#1-telegram)
  - [1.2 Problem](#12-problem)
  - [1.3 Problem recovery](#13-problem-recovery)
- [2. Gmail](#2-gmail)
- [3. Khác](#3-khác)
- [Tài liệu tham khảo](#tài-liệu-tham-khảo)

# 1. Telegram

- Chọn: `Administration > Media types`
- Chọn `Telegram`

![Imgur](https://i.imgur.com/6ArUMzm.png)

- Chọn `Message templates`, danh sách các message type hiện ra. Chọn `Edit` vào loại muốn chỉnh sửa.

![Imgur](https://i.imgur.com/1LMKPd3.png)
- Ta quan tâm đến 2 loại:
  - Problem: Cảnh báo khi sảy ra vấn đề
  - Problem recovery: Cảnh báo khi vấn đề được giải quyết
## 1.2 Problem
> Sử dụng: html
- Tỉnh chỉnh đơn giản:
```
Subject: <b>PROBLEM:{TRIGGER.NAME}</b>
Message:
            <b>Host:</b>  {HOST.NAME}
            <b>IP:</b> {HOST.IP}
            <b>Severity:</b>  {TRIGGER.SEVERITY}
            <b>Time:</b>  {EVENT.TIME} {EVENT.DATE}
            <b>Last value:</b> {ITEM.LASTVALUE}
```
![Imgur](https://i.imgur.com/fqcC6Od.png)

- Trong đó:
  - `{TRIGGER.NAME}`: Tên của vấn đề xảy ra
  - `{HOST.IP}`: Địa chỉ IP của thiết bị xảy ra vấn đề
  - `{TRIGGER.SEVERITY}`: Mức độ nguy hiểm của Cảnh báo
  - `{EVENT.TIME} {EVENT.DATE}`: Thời gian (giờ, ngày) xảy ra vấn để
  - `{ITEM.LASTVALUE}`: Giá trị `item` cuối được thu thập.`

- Kết quả:
![Imgur](https://i.imgur.com/ne4gV78.png)

- Có thể thêm các Option khác để cảnh báo nếu cần thiết: [Tham khảo tại đây](https://www.zabbix.com/documentation/current/en/manual/appendix/macros/supported_by_location).

## 1.3 Problem recovery
- Cấu trúc bản tin cảnh báo được gửi khi vấn đề được giải quyết:
```
Subject: <b>RESOLVED:{EVENT.NAME}</b>
Message:
            <b>Host</b>: {HOST.NAME}
            <b>IP:</b> {HOST.IP}
            <b>Severity:</b> {EVENT.SEVERITY}
            <b>Time:</b> {EVENT.RECOVERY.TIME}
            <b>Duration issue:</b> {EVENT.DURATION}
```

![Imgur](https://i.imgur.com/h21CP6R.png)

- Trong đó:
  - `{EVENT.NAME}`: Tên của vấn đề
  - `{HOST.IP}`: Địa chỉ IP của thiết bị xảy ra vấn đề
  - `{TRIGGER.SEVERITY}`: Mức độ nguy hiểm của Cảnh báo
  - `{EVENT.RECOVERY.TIME}`: Thời gian vấn đề được giải quyết
  - `{EVENT.DURATION}`: Thời gian từ lúc bắt đầu đến lúc vấn đề được giải quyết.

- Kết quả:

![Imgur](https://i.imgur.com/8N7ccLy.png)

- Có thể thêm các Option khác để cảnh báo nếu cần thiết: [Tham khảo tại đây](https://www.zabbix.com/documentation/current/en/manual/appendix/macros/supported_by_location).
# 2. Gmail
>Thực hiện tương tự
- Problem:

![Imgur](https://i.imgur.com/X0JfXGa.png)

- Recovery:

![Imgur](https://i.imgur.com/14YruSY.png)

# 3. Khác
- [Gửi cảnh báo đồ thị tới telegram](https://github.com/ableev/Zabbix-in-Telegram)

# Tài liệu tham khảo
1. https://github.com/ableev/Zabbix-in-Telegram
2. https://www.zabbix.com/documentation/current/en/manual/appendix/macros
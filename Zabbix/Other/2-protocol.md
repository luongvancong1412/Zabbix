<h1> Protocols </h1>

<h2> Mục lục </h2>

- [1. Passive checks](#1-passive-checks)
- [2. Active checks](#2-active-checks)
  - [2.1 Nhận danh sách các item](#21-nhận-danh-sách-các-item)
  - [2.2 Gửi dữ liệu đã thu thập](#22-gửi-dữ-liệu-đã-thu-thập)
- [Tài liệu tham khảo](#tài-liệu-tham-khảo)

---

Zabbix sử dụng giao thức truyền thông dựa trên JSON để giao tiếp với Zabbix Agent.

# 1. Passive checks
- `Passive check` là một `simple data request`.
  - Server Zabbix (hoặc Proxy) yêu cầu dữ liệu, ví dụ: tải CPU
  - Zabbix Agent sẽ gửi kết quả trở lại Server.

**Server Request**

```
<item key>\n
```


Agent Response
```
<HEADER><DATALEN><DATA>
```

1. Server mở kết nối TCP
2. Server gửi `agent.ping\n`
3. Agent đọc yêu cầu và trả lời bằng `<HEADER> <DATALEN> 1`
4. Server xử lý dữ liệu để nhận giá trị, trong trường hợp này giá trị là `1`
5. Đóng kết nối TCP


# 2. Active checks
- Yêu cầu xử lý phức tạp hơn.
  - Trước tiên, Agent phải truy xuất danh sách các item để xử lý độc lập.
  - Định kỳ gửi các giá trị mới đến Server.

## 2.1 Nhận danh sách các item
1. Agent mở kết nối TCP
2. Agent yêu cầu danh sách các check
3. Server phản hồi bằng danh sách các item (item key, delay)
4. Agent phân tích cú pháp phản hồi
5. Đóng kết nối TCP
6. Agent bắt đầu thu thập dữ liệu định kỳ
## 2.2 Gửi dữ liệu đã thu thập
1. Agent mở kết nối TCP
2. Agent gửi danh sách các giá trị
3. Server xử lý dữ liệu và gửi lại trạng thái
4. Đóng kết nối TCP

# Tài liệu tham khảo

1. https://www.zabbix.com/documentation/1.8/en/protocols/agent
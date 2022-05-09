<h1> Items </h1>

<h2> Mục lục </h2>

- [1. Tổng quan](#1-tổng-quan)
- [2. Tạo 1 item](#2-tạo-1-item)
	- [2.1 Tổng quan](#21-tổng-quan)
	- [2.2 Cấu hình chi tiết](#22-cấu-hình-chi-tiết)
	- [2.3 Testing](#23-testing)
- [Tài liệu tham khảo](#tài-liệu-tham-khảo)

# 1. Tổng quan
- Item là dữ liệu thu thập từ một host
  - `system.cpu.load` : sẽ thu thập dữ liệu tải của bộ xử lý
  - `net.if.in` :thu thập thông tin lưu lượng đến.

- Để thêm các tham số khác, viết chúng trong dấu ngoặc vuông sau tên khóa.
  - `system.cpu.load [avg5]` sẽ trả về mức trung bình tải của bộ xử lý trong 5 phút qua
  - `net.if.in [eth0]` sẽ hiển thị lưu lượng đến trong giao diện eth0.


# 2. Tạo 1 item

## 2.1 Tổng quan
Các bước tạo item trong giao diện người dùng web:
- Chọn: `Configuration → Hosts`
- Click vào `Items` trong hàng của host muốn tạo item
- Click vào `Create item` ở góc trên bên phải màn hình
- Nhập các thông số của `item` vào form.

## 2.2 Cấu hình chi tiết
- Tab Item chứa các thuộc tính chung của item.

<p align="center">
<img src=https://i.imgur.com/pClv2ip.png>
</p>

<p align="center">
<img src=https://i.imgur.com/evIc0nW.png>
</p>

<p align="center">
<img src=https://i.imgur.com/clwoRSl.png>
</p>

- Tất cả các trường bắt buộc được đánh dấu bằng dấu hoa thị `*` màu đỏ.

STT|Tham số|Mô tả
|:---:|:---:|---|
1|`Name`|Tên item.
2|`Type`|Loại item.
3|`Key`|Item key (tối đa 2048 ký tự).<br>Key phải là duy nhất trong một host duy nhất.<br>Nếu key type là `Agent Zabbix`, `Agent Zabbix (active)` hoặc `Simple check`, thì giá trị key phải được hỗ trợ bởi Agent Zabbix hoặc Zabbix server.
4|`Type of information`|Loại dữ liệu được lưu trữ trong cơ sở dữ liệu sau khi thực hiện chuyển đổi, nếu có.<br>+ `Numeric (unsigned)` - Số nguyên không dấu 64 bit.<br>+ `Numeric(float)` - Số thực 64 bit
5|`Host interface`| Chọn giao diện host. Trường này có sẵn khi chỉnh sửa một item ở cấp độ host.
6|`Units`|Các đơn vị. Nếu unit được đặt, Zabbix sẽ thêm post processing  vào giá trị nhận được và hiển thị nó với mã unit đã đặt.<br>Theo mặc định, nếu giá trị raw vượt quá 1000 sẽ được chia cho 1000 và được hiển thị tương ứng.<br>Ví dụ: nếu đặt bps và có giá trị là 881764, sẽ được hiển thị là 881,76 Kbps.<br>Tiêu chuẩn bộ nhớ JEDEC được sử dụng để xử lý các đơn vị B(byte), Bps (byte trên giây), được chia cho 1024. Do đó, nếu đơn vị được đặt thành B hoặc Bps , Zabbix sẽ hiển thị:<br>1 là 1B/1Bps<br>1024 là 1KB/1KBps<br>1536 dưới dạng 1.5KB/1.5KBps<br>Các đơn vị liên quan đến thời gian sau:<br>`unixtime` - được dịch thành "yyyy.mm.dd hh:mm:ss". Để dịch chính xác, giá trị nhận được phải là `Nummeric (unsigned)` - loại thông tin Số (không dấu) .<br>`uptime` - được dịch thành "hh:mm:ss" hoặc "N day, hh:mm:ss"<br>Ví dụ: nếu giá trị là 881764 (giây), sẽ được hiển thị là "10 dáy, 04:56:04 "<br>`s` - được dịch thành" yyy mmm ddd hhh mmm sss ms "; tham số được coi là số giây.<br>Ví dụ: nếu nhận được giá trị là 881764 (giây), sẽ được hiển thị là "10 ngày 4 giờ 56 phút".<br>Sẽ được dịch thành "< 1 ms" nếu giá trị nhỏ hơn 0,001.
7|`Update interval`|Cập nhật khoảng thời gian. Lấy một giá trị mới cho item này sau mỗi N giây. Update interval tối đa cho phép là 86400 giây (1 ngày).<br>Các hậu tố thời gian được hỗ trợ, ví dụ: 30s, 1m, 2h, 1d.
8|`Custom intervals`|Khoảng thời gian tùy chỉnh. Có thể tạo các quy tắc tùy chỉnh để kiểm tra item:<br>Flexible - tạo ngoại lệ cho Update interval (khoảng thời gian với tần suất khác nhau)<br>Scheduling - tạo lịch polling tùy chỉnh.
9|`Trend storage period`|Chọn một trong hai:<br>`Do not keep trends` (Không lưu lịch sử)<br>`Storage period` (Thời gian lưu trữ) - chỉ định khoảng thời gian lưu giữ lịch sử chi tiết trong cơ sở dữ liệu (1 giờ đến 25 năm).
10|`Value mapping`|	Áp dụng ánh xạ giá trị cho item này. Value mapping không thay đổi các giá trị đã nhận, nó chỉ để hiển thị dữ liệu.<br>Nó hoạt động với các item `Numeric (unsigned)` , `Numeric (float)` và `Character` .
11|`Log time format`|Định dạng thời gian ghi nhật ký. Chỉ có sẵn cho các item thuộc loại Log. Hỗ trợ:<br>* y : Năm (1970-2038)<br>* M : Tháng (01-12)<br>* d : Ngày (01-31)<br>* h : Giờ (00-23)<br>* m : Phút (00-59)<br>* s : Thứ hai (00-59)<br>Ví dụ:`23480:20100328:154718.045 Zabbix agent started. Zabbix 1.8.2 (revision 11211).`<br>Bắt đầu với sáu vị trí ký tự cho PID, tiếp theo là ngày, giờ và phần còn lại của dòng.<br>Định dạng thời gian ghi nhật ký cho dòng này sẽ là "pppppp: yyyyMMdd: hhmmss".
12|`Populates host inventory field`|Có thể chọn giá trị của item sẽ được điền vào. Điều này sẽ hoạt động nếu nó bật cho host.
13|`Description`|	Nhập mô tả item.|
14|`Enabled`|Đánh dấu vào box để bật mục để item đó sẽ được xử lý.
15|`Latest date`|Xem dữ liệu mới nhất cho item.|

## 2.3 Testing
- Có thể kiểm tra một item xem có được định cấu hình đúng không, nếu đúng sẽ nhận được một giá trị thực. Kiểm tra có thể xảy ra ngay cả trước khi một item được lưu.

- Testing có sẵn cho các template item và host, item prototypes and low-level discovery rules. Testing không khả dụng cho các mục đang hoạt động.

- Kiểm tra mục có sẵn cho các loại item passive sau:
  - Zabbix agent
  - SNMP agent (v1, v2, v3)
  - IPMI agent
  - SSH checks
  - Telnet checks
  - JMX agent
  - Simple checks (except icmpping*, vmware.* items)
  - Zabbix internal
  - Calculated items
  - External checks
  - Database monitor
  - HTTP agent
  - Script

- Để kiểm tra một item, hãy nhấp vào nút Test ở cuối form  trong cấu hình item.

>Lưu ý rằng nút Kiểm tra sẽ bị vô hiệu hóa đối với các mục không thể kiểm tra (như kiểm tra hoạt động, loại trừ kiểm tra đơn giản).

# Tài liệu tham khảo

1. https://www.zabbix.com/documentation/current/en/manual/config/items/item

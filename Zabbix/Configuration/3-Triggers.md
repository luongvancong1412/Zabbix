<h1> Triggers </h1>

<h2> Mục lục </h2>

- [1. Tổng quan](#1-tổng-quan)
  - [1.1 Trigger là gì?](#11-trigger-là-gì)
  - [1.2 Các trạng thái của Trigger](#12-các-trạng-thái-của-trigger)
  - [1.3 Thời gian tính toán](#13-thời-gian-tính-toán)
  - [1.4 Thời gian đánh giá](#14-thời-gian-đánh-giá)
- [2. Config một trigger](#2-config-một-trigger)
  - [2.1 Tổng quan](#21-tổng-quan)
  - [2.2 Chi tiết cấu hình](#22-chi-tiết-cấu-hình)
- [Tài liệu tham khảo](#tài-liệu-tham-khảo)


# 1. Tổng quan
## 1.1 Trigger là gì?
- Triggers là:
  - biểu thức logic
  - `đánh giá` dữ liệu được thu thập bởi các item
  - và đại diện cho trạng thái system hiện tại.

- Trigger dùng để kích hoạt trạng thái dữ liệu từ `acceptable` thành `PROBLEM`
  - Trigger expressions - Biểu thức kích hoạt xác định ngưỡng trạng thái dữ liệu là `acceptable` (chấp nhận được).
  - Nếu dữ liệu đến vượt qua trạng thái `acceptable`, một trigger sẽ được kích hoạt (`fired`) - hoặc thay đổi status thành `PROBLEM` (có vấn đề).

## 1.2 Các trạng thái của Trigger

|STT|Value|Description|
|:---:|:---:|---|
1|`OK`|	Trạng thái bình thường.
2|`PROBLEM`|	Có một vấn đề gì đó đã xảy ra.|

- Trong một trigger cơ bản, có thể đặt ngưỡng cho mức trung bình khoảng năm phút của một số dữ liệu
  - Ví dụ: CPU load. Điều này được thực hiện bằng một biểu thức trigger trong đó:
    - Ap dụng hàm `avg` cho giá trị nhận được trong item key
    - Sử dụng khoảng thời gian năm phút để `đánh giá`
    - Đặt một ngưỡng là `2`.

    ```
    avg(host/key,5m)>2
    ```
  - Trigger này sẽ "kích hoạt" (`PROBLEM`) nếu mức trung bình năm phút lớn hơn 2.

- Trong một trigger `phức tạp` hơn, biểu thức có thể bao gồm sự kết hợp của `nhiều hàm` và `nhiều ngưỡng`.

- Hầu hết các hàm trigger được đánh giá dựa trên dữ liệu lịch sử , trong khi một số hàm trigger cho phân tích dài hạn, ví dụ: `trendavg()` , `trendcount()` , v.v., sử dụng dữ liệu trend.

## 1.3 Thời gian tính toán
- Một `trigger` được tính toán lại mỗi khi `Zabbix server` nhận được giá trị mới là một phần của biểu thức. 
- Khi một giá trị mới được nhận, mỗi hàm có trong biểu thức sẽ được tính toán lại.
- Các hàm dựa trên thời gian là `nodata( )` , `date()` , `dayofmonth()` , `dayofweek()` , `time()` , `now()`); chúng được tính toán lại sau `mỗi 30 giây` bằng quy trình đồng bộ hóa lịch sử Zabbix.


## 1.4 Thời gian đánh giá
- Khoảng thời gian đánh giá được sử dụng trong các chức năng tham chiếu item history.
- Nó có thể được xác định dưới dạng 
  - Khoảng thời gian (30s, 10m, 1h)
  - Phạm vi giá trị (#5 - cho năm giá trị mới nhất).

# 2. Config một trigger
## 2.1 Tổng quan

- Các bước configure một trigger:
  - Chọn: `Configuration → Hosts`
  - Click vào `Trigger` trong hàng của host
- Click vào `Create trigger` ở bên phải (hoặc click vào tên của trigger để chỉnh sửa trigger)
- Nhập các thông số của trigger vào biểu mẫu

## 2.2 Chi tiết cấu hình
`Tab Trigger` chứa tất cả các thuộc tính trigger cần thiết .

![Imgur](https://i.imgur.com/2cqzXji.png)

STT|Parameter|Description|
|:---:|:---:|---|
1|`Name`|	Tên của trigger.<br>Các macro được hỗ trợ là:`{HOST.HOST}`, `{HOST.NAME}`, `{HOST.PORT}`, `{HOST.CONN}`, `{HOST.DNS}`, `{HOST.IP}`, `{ITEM.VALUE}`, `{ITEM.LASTVALUE}`, `{ITEM.LOG.*}` và `{$MACRO}` .<br>Các macro `$1`, `$2` ... `$9` có thể được sử dụng để tham chiếu đến hằng số thứ nhất, thứ 2 ... thứ 9 của biểu thức.<br>Ví dụ: tên `Processor load above $1 on {HOST.NAME}` sẽ tự động thay đổi thành `Processor load above 5 on New host` nếu biểu thức là cuối cùng `(/Newhost/system.cpu.load[percpu,avg1])>5`
2|`Event name`|Nếu được xác định, tên này sẽ được sử dụng để `tạo tên sự kiện sự cố`, thay vì `tên trigger`.
3|`Operational data`|Dữ liệu hoạt động cho phép xác định các chuỗi tùy ý cùng với các macro. <br>Các macro sẽ tự động giải quyết dữ liệu thời gian thực trong `Monitoring → Problems` . 
4|`Severity`|	Đặt `mức độ nghiêm trọng` của trigger cần thiết.
5|`Expression`|Biểu thức logic được sử dụng để xác định các điều kiện của một `problem`.<br>Một `PROBLEM` được tạo ra sau khi biểu thức đánh giá (`Expression evaluates`) là `TRUE` (tất cả `điều kiện` trong biểu thức `đúng`). Sự cố sẽ được giải quyết ngay sau khi `expression evaluates` là `FALSE`.
6|`OK event generation`|	Các tùy chọn tạo sự kiện OK:<br>+ `Expression` - Các sự kiện OK được tạo dựa trên expression giống như các problem event;<br>+ `Recovery expression` (Biểu thức khôi phục) - OK events được tạo nếu problem expression evaluetes là FALSE và recovery expression evaluetes là TRUE;<br>+ `None` - trong trường hợp này, trigger sẽ không tự trở lại trạng thái OK.
7|`Recovery expression`|	Biểu thức logic (tùy chọn) xác định các điều kiện bổ sung phải được đáp ứng để `PROBLEM` được giải quyết, sau khi `problem expression` ban đầu đã được đánh giá là `FALSE`.<br> Không thể giải quyết sự cố chỉ bằng `Recovery expression` nếu `problem expression` vẫn là `TRUE`. Trường này chỉ có sẵn nếu `Recovery expression` được chọn để tạo `OK event`.
8|`PROBLEM event generation mode`|Chế độ tạo `PROBLEM events`:<br>+ `Single` - một event duy nhất được tạo khi trigger chuyển sang trạng thái `PROBLEM` lần đầu tiên;<br>+ `Multiple` - một event được tạo dựa trên mọi `PROBLEM` evaluation của Trigger.
9|`OK event closes`|	Chọn nếu `OK event` đóng lại:<br>+ `All problems` - tất cả problem của Trigger này.<br>+ `All problems if tag values match`
10|`Allow manual close`|Có thể đóng thủ công khi ghi nhận các `PROBLEM event`.
11|`Description`|Cung cấp `thêm thông tin về trigger`.<br>Có thể chứa hướng dẫn để khắc phục sự cố cụ thể, chi tiết liên hệ của nhân viên chịu trách nhiệm, v.v.
12|`Enabled`|Bỏ chọn box để `vô hiệu hoá Trigger` này.<br>Các PROBLEM không còn hiển thị trong giao diện người dùng, nhưng không bị xóa.|


# Tài liệu tham khảo

1. https://www.zabbix.com/documentation/current/en/manual/config/triggers


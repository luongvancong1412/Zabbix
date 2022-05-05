<h1> Thêm Trigger</h1>

<h2> item lục</h2>

- [1. Tổng quan](#1-tổng-quan)
- [2. Thêm trigger](#2-thêm-trigger)
- [3. Hiển thị trạng thái trigger](#3-hiển-thị-trạng-thái-trigger)
- [Tài liệu tham khảo](#tài-liệu-tham-khảo)

# 1. Tổng quan
- Các `item` chỉ thu thập dữ liệu. Để tự động đánh giá dữ liệu đến cần xác định các `trigger`. 
- Một `Trigger` chứa một `biểu thức xác định ngưỡng` - là mức có thể chấp nhận được đối với dữ liệu.

- Nếu `mức` đó `bị vượt qua` bởi dữ liệu đến, `trigger` sẽ "kích hoạt" (fire) hoặc chuyển sang trạng thái `Sự cố` (`Problem`) - cho biết rằng điều gì đó đã xảy ra có thể cần được chú ý. - Nếu mức lại được chấp nhận, `trigger` trở về trạng thái `Ok`.

# 2. Thêm trigger
- Để cấu hình `trigger` cho `item`, Chuyển tới `Configuration` → `Hosts` , tìm `Host` cần thêm `trigger` và click vào `Trigger` bên cạnh nó, sau đó nhấp vào `Create trigger` .

<p align="center">
<img src=https://i.imgur.com/NvJ8SdC.png>
</p>

<p align="center">
<img src=https://i.imgur.com/6cihLIo.png>
</p>

Các trường cơ bản cần chú ý là: `Name`, `Experssion`

<h3>Name</h3>

- Nhập `CPU load too high on 'New host' for 3 minutes`
- Đây sẽ là `tên Trigger` được hiển thị trong danh sách và các nơi khác.

<p align="center">
<img src=https://i.imgur.com/vUUuezV.png>
</p>

<h3>Experssion</h3>

<p align="center">
<img src=https://i.imgur.com/mPdmjHd.png>
</p>

- Nhập: `avg(/New host/system.cpu.load,3m)>2`

<p align="center">
<img src=https://i.imgur.com/hR5hXWt.png>
</p>

- Đây là biểu thức kích hoạt (`trigger expression`). `Item key` ở đây (`system.cpu.load`) được sử dụng để tham chiếu đến `item`
- Biểu thức cụ thể này về cơ bản nói rằng `ngưỡng sự cố bị vượt quá` khi `giá trị trung bình tải của CPU` `trong 3 phút` `vượt quá 2`. 
- Bạn có thể tìm hiểu thêm về `cú pháp của biểu thức kích hoạt` ([syntax of trigger expressions](https://www.zabbix.com/documentation/current/en/manual/config/triggers/expression)).

<p align="center">
<img src=https://i.imgur.com/vmErIcY.png>
</p>

Cuối cùng, click vào `Add` . `Trigger` mới sẽ xuất hiện trong danh sách `trigger`.

<p align="center">
<img src=https://i.imgur.com/VR7TJUr.png>
</p>

# 3. Hiển thị trạng thái trigger
- Với một `Trigger` được xác định, có thể xem trạng thái của nó.

- Nếu tải CPU đã vượt quá mức ngưỡng bạn đã xác định trong `trigger`, sự cố sẽ được hiển thị trong `Monitering` → `Problems` .

<p align="center">
<img src=https://i.imgur.com/3FislEP.png>
</p>

Nhấp nháy trong cột trạng thái cho biết trạng thái kích hoạt thay đổi gần đây, trạng thái đã diễn ra trong `30 phút` qua.

- Trong trường hợp này là Centos 7 tắt quá 10 phút

<p align="center">
<img src=https://i.imgur.com/XS4MCLc.png>
</p>

<p align="center">
<img src=https://i.imgur.com/0V7y8vP.png>
</p>

# Tài liệu tham khảo

1. https://www.zabbix.com/documentation/current/en/manual/quickstart/trigger
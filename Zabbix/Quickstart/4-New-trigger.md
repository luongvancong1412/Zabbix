<h1> Thêm Trigger</h1>

<h2> Mục lục</h2>


# 1. Tổng quan
- Các item chỉ thu thập dữ liệu. Để tự động đánh giá dữ liệu đến cần xác định các trigger. 
- Một Trigger chứa một biểu thức xác định ngưỡng - là mức có thể chấp nhận được đối với dữ liệu.

- Nếu mức đó bị vượt qua bởi dữ liệu đến, trigger sẽ "kích hoạt" (fire) hoặc chuyển sang trạng thái `Sự cố` (`Problem`) - cho biết rằng điều gì đó đã xảy ra có thể cần được chú ý. - Nếu mức lại được chấp nhận, trigger trở về trạng thái `Ok`.

# 2. Thêm trigger
- Để cấu hình trigger cho item, Chuyển tới Configuration → Hosts , tìm `Host` cần thêm trigger và click vào Trigger bên cạnh nó, sau đó nhấp vào Create trigger .


Các trường cơ bản cần chú ý là:

<h3>Name</h3>

- Nhập tải CPU quá cao trên 'Máy chủ mới' trong 3 phút làm giá trị. 
- Đây sẽ là tên Trigger được hiển thị trong danh sách và các nơi khác.

<h3>Experssion</h3>

- Nhập: avg (/New host/system.cpu.load,3m)>2

- Đây là biểu thức kích hoạt (trigger expression). Item key ở đây (system.cpu.load) được sử dụng để tham chiếu đến item
- Biểu thức cụ thể này về cơ bản nói rằng ngưỡng sự cố bị vượt quá khi giá trị trung bình tải của CPU trong 3 phút vượt quá 2. Bạn có thể tìm hiểu thêm về `cú pháp của biểu thức kích hoạt` (link).

Cuối cùng, click vào Add . Trigger mới sẽ xuất hiện trong danh sách trigger.

# 3. Hiển thị trạng thái trigger
- Với một Trigger được xác định, có thể xem trạng thái của nó.

- Nếu tải CPU đã vượt quá mức ngưỡng bạn đã xác định trong trigger, sự cố sẽ được hiển thị trong Monitering → Problems .



Nhấp nháy trong cột trạng thái cho biết trạng thái kích hoạt thay đổi gần đây, trạng thái đã diễn ra trong 30 phút qua.


# Tài liệu tham khảo

1. https://www.zabbix.com/documentation/current/en/manual/quickstart/trigger
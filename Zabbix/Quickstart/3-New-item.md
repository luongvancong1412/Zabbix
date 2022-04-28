<h1> Thêm Item </h1>

<h2> Mục lục </h2>

- [1. Tổng quan](#1-tổng-quan)
- [2. Thêm item](#2-thêm-item)
- [3. Xem dữ liệu](#3-xem-dữ-liệu)
- [4. Đồ thị (Graphs)](#4-đồ-thị-graphs)
- [Tài liệu tham khảo](#tài-liệu-tham-khảo)

# 1. Tổng quan
- Các `item` là `cơ sở` thu thập dữ liệu trong Zabbix. 
- `Không có` item, sẽ không có `dữ liệu` - vì một `item` xác định một chỉ số `duy nhất` hoặc `loại dữ liệu` cần thu thập từ host.

# 2. Thêm item
- Tất cả các item được nhóm xung quanh các host. Đó là lý do tại sao để cấu hình một item mẫu, vào `Configuration` → `Hosts` và tìm host vừa tạo hoặc host đã tạo.

<p align="center">
<img src=https://i.imgur.com/SSOtKG4.png>
</p>

- Click vào liên kết item trong hàng của `host` cần thêm item, sau đó click vào `Create item`.

<p align="center">
<img src=https://i.imgur.com/zFQg3AV.png>
</p>



<p align="center">
<img src=https://i.imgur.com/7t1LK46.png>
</p>


- Tất cả các trường `bắt buộc` được đánh dấu bằng dấu hoa thị `*` màu đỏ.

Đối với `item` mẫu, thông tin cơ bản cần thiết là: Name, Key và Type of information

<p align="center">
<img src=https://i.imgur.com/Sccv6KG.png>
</p>


<h3> Name</h3>

- Đây là `tên item` sẽ `được hiển thị` trong danh sách và các nơi khác.
- Nhập tải CPU làm giá trị. 

<h3>Key</h3>

- Nhập system.cpu.load theo cách thủ công làm giá trị. 
- Đây là tên kỹ thuật (`technical name`) của một item x`ác định loại thông tin` sẽ được `thu thập`.
- Key cụ thể (`particular key`) chỉ là một trong các` key được xác định trước` đi `kèm với Agent` Zabbix.

<h3>Type of information</h3>

- Thuộc tính này `xác định định dạng` của `dữ liệu` mong đợi. 
- Đối với khóa system.cpu.load , trường này sẽ tự động được đặt thành Numeric (float) .
 
> Note:Bạn cũng có thể muốn giảm số ngày lịch sử mục sẽ được lưu giữ, xuống còn 7 hoặc 14. Đây là một phương pháp hay để cơ sở dữ liệu không lưu giữ nhiều giá trị lịch sử.

- Các `tùy chọn khác để mặc định` (phù hợp trong phần Quickstart)

- Cuối cùng, Click vào `Add` . `Item` mới sẽ xuất hiện trong danh sách item.
- Click vào `Details` phía trên danh sách để `xem chi tiết` những gì thực hiện.


<p align="center">
<img src=https://i.imgur.com/c082cVU.png>
</p>




# 3. Xem dữ liệu
- Để xem một item `có thu thập dữ liệu không`, Chuyển đến `Monitoring` → `Latest data` , chọn `host` vừa thêm trong filter và  click vào `Apply`.

https://i.imgur.com/GbuFT02.png

- Theo mặc định cần 60s (chu kỳ) server đọc các thay đổi cấu hình và chọn các item mới để thực thi (execute).

- Nếu không thấy giá trị nào trong cột `Change`, có thể cho đến giờ bạn chỉ nhận được một giá trị. Chờ 30s để giá trị khác đến.

https://i.imgur.com/j92Ylo0.png

- Nếu bạn không thấy thông tin về item như trong ảnh chụp màn hình, hãy đảm bảo rằng:

- Đã điền vào các trường `Key` và `Type of information` chính xác như trong ảnh chụp màn hình
- Cả `Agent` và `server` đều đang chạy
- trạng thái host là `Monitored` (Được theo dõi) và biểu tượng `Availability` của nó có màu `xanh lá cây`.
- một host được chọn trong danh sách `host dropdown`, item là active.

# 4. Đồ thị (Graphs)
- Với item hoạt động trong một thời gian, đã đến lúc cần nhìn thấy thứ gì đó trực quan. 
- `Simple graphs` có sẵn cho bất kỳ item được giám sát nào mà không cần bất kỳ cấu hình bổ sung nào.

- Để xem biểu đồ, chuyển đến Monitoring → Latest data và click vào liên kết `Graph` bên cạnh item.

<p align="center">
<img src=https://i.imgur.com/wnnjrqc.png>
</p>

<p align="center">
<img src=https://i.imgur.com/R9GEjV6.png>
</p>



# Tài liệu tham khảo

1. https://www.zabbix.com/documentation/current/en/manual/quickstart/item
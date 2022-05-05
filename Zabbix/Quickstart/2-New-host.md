<h1> Thêm hosts </h1>

<h2> item lục </h2>


# 1. Tổng quan

Bài này viết về cách thiết lập một host mới (new host).

- Host trong Zabbix là một thực thể (`entity`) được `nối mạng` (Physical, virtual) mà bạn muốn `giám sát`.
- Nó có thể là một host vật lý (`physical server`), một bộ chuyển mạch (`a network switch`), một máy ảo (`a virtual machine`) hoặc một số ứng dụng (`some application`).

# 2. Thêm host
- `Thông tin` về các `host` được cấu hình trong Zabbix: `Configuration` → `Hosts` và `Monitoring` → `Hosts` . 
- Có `một host` được xác định trước (`pre-defined`), được gọi là `Zabbix server`. Chính là `server` cài `zabbix-server`.

- Để thêm một host mới, Chọn `Create host` .


<p align="center">
  <img src=https://i.imgur.com/RPgUZXA.png >
</p>


- Cửa sổ cấu hình host xuất hiện.

<p align="center">
<img src=https://i.imgur.com/QrlpngA.png>
</p>

- Các trường bắt buộc được đánh dấu bằng dấu hoa thị `*` màu đỏ.

<h3>Một số trường cần thiết:</h3>

- **Host name:**
  - Nhập tên host. 
  - Cho phép sử dụng `chữ` và `số`, `dấu cách`, `dấu chấm`, `dấu gạch ngang` và `dấu gạch dưới`.

- **Groups:**
  - Select `một` hoặc `một số nhóm` hiện có bằng cách click vào nút Select hoặc `nhập tên nhóm không tồn tại` để tạo `nhóm mới`.

> Note: *Trong Zabbix, tất cả **các quyền truy cập** (access permission) được chỉ định cho **host groups**, không phải **host riêng lẻ**. Vì vậy **một host** phải **thuộc** ít nhất **một nhóm**.*

- **Interface: IP address**
  - Nhập địa chỉ IP của host cần giám sát. 
  - Và nó phải được cấu hình trong  file config agent với directive là `Server`.


- **Các tùy chọn khác** để mặc định.


Cuối cùng, chọn  `Add` để hoàn tất. Host mới sẽ được hiển thị trong danh sách host.

<p align="center">
<img src=https://i.imgur.com/NddV6xh.png>
</p>

<h3> Trường Availability </h3> <img src=https://i.imgur.com/eZ3L3Vv.png width=10% align="right">

- Cột Tính khả dụng (`Availability`) chứa các `cảnh báo` về tính khả dụng của host trên mỗi interface. 
- Được hiển thị bằng biểu tượng `ZBX`:

<br>
<br>
<br>

|**Availability**| **Mô tả**|
|:---:|---|
|![Imgur](https://i.imgur.com/WCLuTqW.png)|Trạng thái `host chưa được thiết lập`;<br>`Chưa có kiểm tra số liệu` nào xảy ra|
|![Imgur](https://i.imgur.com/5dWlcNB.png)|`Host` khả dụng (`Available`);<br>Kiểm tra số liệu (`metric check`) đã thành công (`successful`)|
|![Imgur](https://i.imgur.com/X3gKIb1.png)|`Host` không khả dụng (`Unavailable`);<br>Kiểm tra số liệu `không thành công` (di chuyển con trỏ chuột qua biểu tượng để xem thông báo lỗi).<br>Có thể có một số lỗi với giao tiếp (có thể do thông tin xác thực `interface` không chính xác).<br>Kiểm tra xem `Zabbix server` có `đang chạy` hay `không` và thử `làm mới trang` sau.|


# Tài liệu tham khảo

1. https://www.zabbix.com/documentation/current/en/manual/quickstart/host
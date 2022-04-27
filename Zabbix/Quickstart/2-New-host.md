<h1> Thêm hosts </h1>

<h2> Mục lục </h2>


# 1. Tổng quan

Bài này viết về cách thiết lập một máy chủ mới (new host).

- Host trong Zabbix là một thực thể (`entity`) được `nối mạng` (Physical, virtual) mà bạn muốn `giám sát`.
- Nó có thể là một máy chủ vật lý (`physical server`), một bộ chuyển mạch (`a network switch`), một máy ảo (`a virtual machine`) hoặc một số ứng dụng (`some application`).

# 2. Thêm host
- `Thông tin` về các `host` được cấu hình trong Zabbix: `Configuration` → `Hosts` và `Monitoring` → `Hosts` . 
- Có `một host` được xác định trước (`pre-defined`), được gọi là `Zabbix server`. Chính là `server` cài `zabbix-server`.

- Để thêm một host mới, Chọn `Create host` .

<img src=https://i.imgur.com/RPgUZXA.png align=center>



- Cửa sổ cấu hình host xuất hiện.

<img src=https://i.imgur.com/QrlpngA.png align=center>


- Các trường bắt buộc được đánh dấu bằng dấu hoa thị `*` màu đỏ.

Một số trường cần thiết:

- **Host name:**
  - Nhập tên host. 
  - Cho phép sử dụng `chữ` và `số`, `dấu cách`, `dấu chấm`, `dấu gạch ngang` và `dấu gạch dưới`.

- **Groups:**
- Select `một` hoặc `một số nhóm` hiện có bằng cách click vào nút Select hoặc `nhập tên nhóm không tồn tại` để tạo `nhóm mới`.

> Note: *Trong Zabbix, tất cả **các quyền truy cập** (access permission) được chỉ định cho **host groups**, không phải **host riêng lẻ**. Vì vậy **một host** phải **thuộc** ít nhất **một nhóm**.*

- **Interface: IP address**

- Nhập địa chỉ IP của host cần giám sát. 
- Và nó phải được cấu hình trong  file config agent với directive là `Server`.


- Các tùy chọn khác để mặc định.

- Cuối cùng, chọn  `Add` để hoàn tất. Host mới sẽ được hiển thị trong danh sách host.



<h3> Trường Availability </h3>

<img src=https://i.imgur.com/eZ3L3Vv.png width=20% align="right">

- Cột Tính khả dụng (`Availability`) chứa các `cảnh báo` về tính khả dụng của host trên mỗi interface. 
- Được hiển thị bằng biểu tượng `ZBX`:

Availability| Mô tả|
|:---:|---|
|


- trạng thái máy chủ chưa được thiết lập; chưa có kiểm tra số liệu nào xảy ra
icon_zbx_green.png- máy chủ lưu trữ có sẵn, kiểm tra số liệu đã thành công
icon_zbx_red.png- máy chủ lưu trữ không khả dụng, kiểm tra số liệu không thành công (di chuyển con trỏ chuột qua biểu tượng để xem thông báo lỗi). Có thể có một số lỗi với giao tiếp, có thể do thông tin xác thực giao diện không chính xác. Kiểm tra xem máy chủ Zabbix có đang chạy hay không và thử làm mới trang sau.
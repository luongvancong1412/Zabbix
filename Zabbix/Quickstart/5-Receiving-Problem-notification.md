<h1> Nhận thông báo sự cố </h1>

<h2> Mục lục </h2>

- [1. Tổng quan](#1-tổng-quan)
- [2. Cài đặt e-mail](#2-cài-đặt-e-mail)
- [3. New Action](#3-new-action)
- [4. Nhận thông báo](#4-nhận-thông-báo)
- [Tài liệu tham khảo](#tài-liệu-tham-khảo)

# 1. Tổng quan
- Bài viết này sẽ hướng dẫn `cách thiết lập cảnh báo` dưới dạng `thông báo` trong Zabbix.

- Với các item thu thập dữ liệu (`collecting data`) và trình `trigger` được thiết kế để "chữa cháy" (`fire`) khi có tình huống `xảy ra sự cố`, sẽ `hữu ích` nếu có sẵn một số `cơ chế cảnh báo` để `thông báo về các sự kiện quan trọng` ngay cả khi `không trực tiếp xem giao diện người dùng` của Zabbix.

- `E-mail` là phương thức gửi thông báo sự cố `phổ biến` nhất.

# 2. Cài đặt e-mail
- Ban đầu, có một số phương thức gửi thông báo được xác định trước trong Zabbix. `E-mail` là một trong số đó.

- Để `cấu hình cài đặt e-mail`, hãy chuyển đến `Administration` →` Media type` và click vào `Email` trong danh sách các `media type` được xác định trước.

<p align="center">
<img src=https://i.imgur.com/7RyrTMS.png>
</p>


Tất cả các trường bắt buộc được đánh dấu bằng dấu hoa thị `*` màu đỏ.

<p align="center">
<img src=https://i.imgur.com/ai6Ro70.png>
</p>


- Đặt các giá trị của `SMTP server`, `SMTP helo` và `SMTP e-mail` phù hợp với môi trường của bạn.


> Note: '`Email SMTP`' sẽ được sử dụng làm địa chỉ `Form` cho các thông báo được gửi từ Zabbix.

- Click `Update` khi đã ready.

- Một loại phương tiện phải được liên kết với người dùng bằng cách xác định địa chỉ gửi cụ thể (giống như chúng tôi đã làm khi định cấu hình người dùng mới ), nếu không, nó sẽ không được sử dụng.

# 3. New Action
- Gửi thông báo (`Delivering notification`) là một trong những hành động thực hiện trong Zabbix. 
- Do đó, để thiết lập thông báo, hãy chuyển đến `Configuration` →` Actions` và click vào `Create action` .

<p align="center">
<img src=https://i.imgur.com/S647Fbx.png>
</p>


<p align="center">
<img src=https://i.imgur.com/40GtmqK.png>
</p>

<p align="center">
<img src=https://i.imgur.com/XYQdynw.png>
</p>

- Tất cả các trường bắt buộc được đánh dấu bằng dấu `*` hoa thị màu đỏ.

- Trong biểu mẫu này, hãy nhập tên cho hành động (Name).


- Nếu chúng tôi không thêm bất kỳ điều kiện cụ thể nào , hành động sẽ được thực hiện khi `có bất kỳ thay đổi kích hoạt` nào từ '`Ok`' thành '`Problem`'.

- Vẫn nên xác định action nên làm - và điều đó được thực hiện trong tab `Operations`.



- Click vào Add trong Operations block, Biểu mẫu mới hiện ra.

<p align="center">
<img src=https://i.imgur.com/IYQzZrK.png>
</p>


Tất cả các trường bắt buộc được đánh dấu bằng dấu hoa thị `*` màu đỏ.

<p align="center">
<img src=https://i.imgur.com/ZbO54P9.png>
</p>


- Tại đây, nhấp vào Add trong block Gửi đến Người dùng và chọn người dùng (user) đã xác định. 
- Chọn 'Email' làm giá trị của (Cent only to )Chỉ gửi đến . 
- Cuối cùng, click vào Add và thao tác sẽ được thêm vào:

<p align="center">
<img src=https://i.imgur.com/elnEwXP.png>
</p>


Đó là tất cả cho một cấu hình action đơn giản.

# 4. Nhận thông báo

Mở bảng điều khiển trên host của bạn và chạy:
```
cat /dev/urandom | md5sum
```
- Đây là lệnh giúp giá trị CPU load tăng lên vượt quá 2 trong vòng 3 phút.

- Tiếp theo đi tới `Monitoring` → `Latest data` và xem các giá trị của 'Tải CPU' đã tăng lên như thế nào. 

<p align="center">
<img src=https://i.imgur.com/xSn6MA3.png>
</p>

- Hãy nhớ rằng, để `trigger` kích hoạt , giá trị '`CPU Load`' phải vượt qua `2` trong `3` phút chạy. Một khi nó xảy ra:

- trong `Monitoring` → `Problems`, sẽ thấy `trigger` với trạng thái '`Problem`' nhấp nháy

<p align="center">
<img src=https://i.imgur.com/tt4EhsE.png>
</p>


- Khi đó sẽ nhận được thông báo sự cố trong `e-mail` đã cấu hình.

> Nếu thông báo không hoạt động:
> - xác minh lại một lần nữa rằng cả cài đặt e-mail và hành động đã được định cấu hình đúng cách
> - đảm bảo rằng người dùng đã tạo ít nhất có quyền đọc trên host đã tạo ra event.
> User, là một phần của nhóm người dùng `Zabbix administrator` ít nhất phải có quyền truy cập đọc vào nhóm máy chủ "máy chủ Linux".
> - Ngoài ra, bạn có thể xem action log bằng cách đi tới `Reports` → `Action log`.

<p align="center">
<img src=https://i.imgur.com/W1RRxil.png>
</p>

# Tài liệu tham khảo

1. https://www.zabbix.com/documentation/current/en/manual/quickstart/notification
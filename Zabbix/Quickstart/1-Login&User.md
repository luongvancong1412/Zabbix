<h1> Đăng nhập và Quản lý người dùng</h1>

<h2> item lục </h2>

- [1. Đăng nhập](#1-đăng-nhập)
  - [1.1 Đăng nhập giao diện web:](#11-đăng-nhập-giao-diện-web)
  - [1.2 Tránh Brute Force Attacks](#12-tránh-brute-force-attacks)
- [2. Quản lý người dùng](#2-quản-lý-người-dùng)
  - [2.1 Thêm người dùng](#21-thêm-người-dùng)
  - [2.2 Thêm quyền](#22-thêm-quyền)
- [Tài liệu tham khảo](#tài-liệu-tham-khảo)

# 1. Đăng nhập
## 1.1 Đăng nhập giao diện web:

- **User/Password default**: `Admin`/`zabbix` - Đăng nhập với quyền `Superuser`

<p align="center">
  <img src="https://i.imgur.com/yYcHD1e.png">
</p>

## 1.2 Tránh Brute Force Attacks 

<img src=https://i.imgur.com/EWnNq0d.png width=30% align="right">


- Kiểu tấn công **Brute Force** là kiểu tấn công được dùng cho tất cả các loại mã hóa. Brute force hoạt động bằng cách thử tất cả các chuỗi mật khẩu có thể để tìm ra mật khẩu. (*Theo wikipedia*)


- Tránh `Brute Force Attacks`, Zabbix:

  - `5 lần` đăng nhập `sai liên tiếp`, sẽ bị `chặn trong 30s` (Kể cả khi đã nhập đúng vẫn không đăng nhập được trong 30s này)
  - Khi đăng nhập thành công, địa chỉ IP của lần đăng nhập không thành công sẽ được hiển thị

    <img src=https://i.imgur.com/PvhtglN.png width=60%>

# 2. Quản lý người dùng
- Xem thông tin user, chọn: `Administration` **>** `Users`

<img src=https://i.imgur.com/ogVem8a.png align=center>

## 2.1 Thêm người dùng
- Thêm người dùng mới, chọn: `Create user`

<p align="center">
<img src=https://i.imgur.com/0RSqPgM.png>
<img src=https://i.imgur.com/mq9cWUN.png>
</p>

- Tất cả các trường bắt buộc bắt đầu bằng dấu `*` màu đỏ.
- Nhập: `Username`, `Name`, `Group`, `Password`, `Password (one again)`, `Time zone` .

<p align="center">
<img src=https://i.imgur.com/mq9cWUN.png>
</p>

<h3>Sang tab Media</h3>

<p align="center">
<img src=https://i.imgur.com/KvwLpf9.png>
</p>

- Chọn `Type` Email (Có thể chọn type khác)
- Nhập địa chỉ email cho người dùng.
- Định khoảng thờig gian Meida hoạt động. Theo mặc định, Media luôn hoạt động
- Cũng có thể tuỳ chỉnh mức độ nghiêm trọng của trigger, tuy nhiên nên để all.
- Nhấn vào `Add` để thêm `Media`, sau đó chuyển sang tab `Permissions`:

<p align="center">
<img src=https://i.imgur.com/7BRMeiE.png>
</p>

- Tab Permissions có 1 trường bắt buộc: `Role`. 

<p align="center">
<img src=https://i.imgur.com/BpL2YDD.png>
</p>

- Bấm Add để thêm người dùng. Người dùng mới sẽ xuất hiện trọng danh sách người dùng.

<p align="center">
<img src=https://i.imgur.com/QwKt6i0.png>
</p>

## 2.2 Thêm quyền
Theo mặc định, user mới không có quyền truy cập host. Để cấp Groups (trong trường hợp này là 'quản trị viên Zabbix'). Trong biểu mẫu thuộc tính nhóm, hãy chuyển đến tab Quyền .

<p align="center">
<img src=https://i.imgur.com/0SOioFZ.png>
</p>

Người dùng này phải có quyền truy cập chỉ đọc vào nhóm host Linux , vì vậy hãy nhấp vào Chọn bên cạnh trường lựa chọn nhóm người dùng.

<p align="center">
<img src=https://i.imgur.com/ljihJCl.png>
</p>

- Trong cửa sổ bật lên này, hãy đánh dấu hộp kiểm bên cạnh `Linux servers`, sau đó nhấp vào `Select` . host Linux sẽ được hiển thị trong trường lựa chọn.

<p align="center">
<img src=https://i.imgur.com/AzECYfm.png>
</p>

- Nhấp vào nút `Read` để đặt cấp độ quyền và sau đó Add để thêm Group vào danh sách quyền. Trong biểu mẫu thuộc tính nhóm người dùng, bấm `Update` .

- Trong Zabbix, quyền truy cập vào host được chỉ định cho các nhóm người dùng , không phải người dùng cá nhân.


# Tài liệu tham khảo

1. https://www.zabbix.com/documentation/current/en/manual/quickstart/login
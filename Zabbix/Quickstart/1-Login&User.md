<h1> Đăng nhập và Quản lý người dùng</h1>

<h2> Mục lục </h2>

- [1. Đăng nhập](#1-đăng-nhập)
  - [1.1 Đăng nhập giao diện web:](#11-đăng-nhập-giao-diện-web)
  - [1.2 Tránh Brute Force Attacks](#12-tránh-brute-force-attacks)
- [2. Quản lý người dùng](#2-quản-lý-người-dùng)
  - [2.1 Thêm người dùng](#21-thêm-người-dùng)
  - [2.2 Phân quyền](#22-phân-quyền)

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
- Xem thông tin user, chọn: `Administration` $\to$ `Users`

## 2.1 Thêm người dùng
- Thêm người dùng mới, chọn: `Create user`
- 
## 2.2 Phân quyền

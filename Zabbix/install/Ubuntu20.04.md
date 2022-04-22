<h1> Zabbix 6.0 LTS: install</h1>

<h2> Mục lục</h2>

- [1. Mô hình mạng](#1-mô-hình-mạng)
- [2. Cài đặt Zabbix Server](#2-cài-đặt-zabbix-server)
  - [2.1 Cài đặt Apache](#21-cài-đặt-apache)
  - [2.2 Cài đặt PHP](#22-cài-đặt-php)
  - [2.3 Cài đặt MariaDB](#23-cài-đặt-mariadb)
  - [2.4 Cầi đặt Zabbix](#24-cầi-đặt-zabbix)
  - [2.5 Cấu hình giao diện người dùng Zabbix](#25-cấu-hình-giao-diện-người-dùng-zabbix)
  - [2.6 Đăng nhập](#26-đăng-nhập)
- [Tài liệu tham khảo](#tài-liệu-tham-khảo)


# 1. Mô hình mạng

# 2. Cài đặt Zabbix Server
## 2.1 Cài đặt Apache
- Tiến hành Update:
```
sudo apt -y update
```
- Cài đặt Apache:
```
sudo apt -y install apache2
```

## 2.2 Cài đặt PHP
- Cài đặt PHP:
```
sudo apt -y install php php-cgi libapache2-mod-php php-common php-pear php-mbstring
```
- Cấu hình Apache2:
```
sudo a2enconf php7.4-cgi
```

```
vi /etc/php/7.4/apache2/php.ini
```
- Sửa dòng 962:
```
date.timezone = "Asia/Ho_Chi_Minh"
```
- Khởi động lại apache2:
```
sudo systemctl restart apache2
```


## 2.3 Cài đặt MariaDB
- Cài đặt gói Mariadb:
```
sudo apt install wget
```
```
wget https://downloads.mariadb.com/MariaDB/mariadb_repo_setup
```
```
echo "b9e90cde27affc2a44f9fc60e302ccfcacf71f4ae02071f30d570e6048c28597 mariadb_repo_setup" \
    | sha256sum -c -
```
```
chmod +x mariadb_repo_setup
```
```
sudo ./mariadb_repo_setup \
   --mariadb-server-version="mariadb-10.5"
```
```
sudo apt update
```
- Cài đặt MariaDB:
```
sudo apt -y install mariadb-server
```
## 2.4 Cầi đặt Zabbix

- Thêm kho lưu trữ Zabbix 6.0:
```
wget https://repo.zabbix.com/zabbix/6.0/ubuntu/pool/main/z/zabbix-release/zabbix-release_6.0-1+ubuntu20.04_all.deb
sudo dpkg -i zabbix-release_6.0-1+ubuntu20.04_all.deb
sudo apt -y update
```
- Cài đặt Zabbix server, frontend, agent:
```
sudo apt -y install zabbix-server-mysql zabbix-frontend-php zabbix-apache-conf zabbix-sql-scripts zabbix-agent
```

- Tạo cơ sở dữ liệu:
```
sudo mysql
```
- Tạo database,user và phân quyền:
```
create database zabbix character set utf8mb4 collate utf8mb4_bin;
create user zabbix@localhost identified by 'zabbix';
grant all privileges on zabbix.* to zabbix@localhost;
quit
```

- Import Cơ sở dữ liệu cho zabbix:
```
cd /usr/share/doc/zabbix-sql-scripts/mysql/
sudo gzip -d server.sql.gz
sudo mysql zabbix < server.sql.gz
```

- Chỉnh sửa tệp `/etc/zabbix/zabbix_server.conf`:
```
sudo vi /etc/zabbix/zabbix_server.conf
```
- Sửa dòng: 100
```
DBName=zabbix
```
- Sửa dòng:
```
DBUser=zabbix
```
- Thêm dòng:
```
DBPassword=zabbix
```
- Khởi động lại Zabbix server, Agent, apache2 và đặt khởi động cùng hệ thống:
```
sudo systemctl restart zabbix-server zabbix-agent apache2
sudo systemctl enable zabbix-server zabbix-agent apache2
```

## 2.5 Cấu hình giao diện người dùng Zabbix
- Sử dụng trình duyệt truy cập: http://server_ip_or_name/zabbix/setup.php

- Chọn `Next step` để bắt đầu cài đặt:

![Imgur](https://i.imgur.com/UbL5kQJ.png)

- Kiểm tra điều kiện: Đảm bảo tất cả các mục đều `[OK]`, Chọn `Next step` để sang bước tiếp theo:

![Imgur](https://i.imgur.com/wRqbM7h.png)


- Cấu hình kết nối với DB: Nhập Database, user và password. Chọn `Next step`

![Imgur](https://i.imgur.com/8wxtJOd.png)

- Cài đặt tên máy chủ, múi giờ và chủ đề cho giao diện người dùng:

![Imgur](https://i.imgur.com/VApJZjK.png)

- Xác nhận các cài đặt trước đó. Chọn `Next step`:

![Imgur](https://i.imgur.com/YzuY4Bl.png)

- Chọn Finish để kết thúc quá trình cài đặt:

![Imgur](https://i.imgur.com/l7PPGmf.png)

## 2.6 Đăng nhập

- Nhập thông tin đăng nhập: Admin/zabbix

![Imgur](https://i.imgur.com/SMsN7SZ.png)

- Đăng nhập thành công:

![Imgur](https://i.imgur.com/FiM3Cct.png)

# Tài liệu tham khảo

1. https://www.server-world.info/en/note?os=Ubuntu_20.04&p=zabbix50&f=1
2. https://www.zabbix.com/documentation/6.0/en/manual/installation/frontend
3. https://www.server-world.info/en/note?os=Ubuntu_20.04&p=zabbix50&f=2
4. https://www.zabbix.com/download?zabbix=6.0&os_distribution=ubuntu&os_version=20.04_focal&db=mysql&ws=apache
5. [Install mariadb 10.5](https://mariadb.com/docs/deploy/topologies/single-node/community-server-10-5/)
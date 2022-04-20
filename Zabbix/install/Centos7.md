<h1> Cài đặt Zabbix trên Centos 7</h1>

<h2> Mục lục</h2>




# 1. Mô hình mạng

![Imgur](https://i.imgur.com/4SK6HLS.png)

- IP Planning:


# 2. Cài đặt Zabbix Server
## 2.1 Cài đặt Apache:

```
yum install -y httpd
```

Cấu hình firewall:
```
firewall-cmd --zone=public --permanent --add-port=80/tcp
firewall-cmd --reload
```

Khởi động dịch vụ:
```
systemctl start httpd
systemctl enable httpd
```

## 2.2 Cài đặt Mariadb
- Thêm Repo:
```
echo '[mariadb]
name = MariaDB
baseurl = http://yum.mariadb.org/10.2/centos7-amd64
gpgkey=https://yum.mariadb.org/RPM-GPG-KEY-MariaDB
gpgcheck=1' >> /etc/yum.repos.d/MariaDB.repo
yum -y update
```

- Cài đặt Mariadb:
```
yum install -y mariadb mariadb-server
```

- Khởi động dịch vụ và cấu hình tường lửa:
```
systemctl start mariadb
systemctl enable mariadb
firewall-cmd --add-service=mysql --permanent
firewall-cmd --reload
```
- Đặt mật khẩu cho root mariadb:

```
mysql_secure_installation
```

## 2.3 Cài đặt PHP
- Cài đặt phiên bản PHP 7.2
```
yum install epel-release -y
```
- Thêm repo:
```
yum install http://rpms.remirepo.net/enterprise/remi-release-7.rpm -y
```
- Cài đặt yum-utils:
```
yum install yum-utils -y
```
- Để cài đặt php 7.2, sử dụng lệnh:
```
yum-config-manager --enable remi-php72
yum update -y
```
- Install các Option php:
```
yum -y install php php-opcache php-mysql
```



## 2.4 Cầi đặt Zabbix
- Install Zabbix repository:
```
rpm -Uvh https://repo.zabbix.com/zabbix/6.0/rhel/7/x86_64/zabbix-release-6.0-1.el7.noarch.rpm
yum clean all
```

- Yum search zabbix:
```
yum search zabbix
```
- Install Zabbix agent:
```
yum install zabbix-agent zabbix-get zabbix-server-mysql zabbix-web-mysql mariadb-server -y
```
```
systemctl start mariadb
mysql
create database zabbix character set uif8 collate utf8_bin;
grant all privileges on zabbix.* to zabbix@localhost identified by 'zabbix';
show databases;

cd /usr/share/doc/zabbix-server-mysql-4.0.5/
ls
zcat create.sql.gz | mysql zabbix

cd
mysql
use zabbix;
show tables;

vi /etc/zabbix/zabbix_server.conf
/DBNa
/DBUs

DBPassword=zabbix
:wq

systemctl start zabbix-server

less /var/log/zabbix/zabbix_server.log

vi /etc/httpd/conf.d/zabbix.conf
bo # trong php_value date.timezone Europe/Riga

systemctl start httpd
``` 
Sử dụng trình duyệt: http://IP/zabbix/setup.php


# Tài liệu tham khảo

1. https://www.zabbix.com/download?zabbix=6.0&os_distribution=centos&os_version=7&db=&ws=
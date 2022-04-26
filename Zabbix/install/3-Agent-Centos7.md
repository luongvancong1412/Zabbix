<h1> Zabbix 6.0 LTS: install</h1>

<h2> Mục lục</h2>

- [1. Mô hình mạng](#1-mô-hình-mạng)
- [2. Centos 7](#2-centos-7)
- [Tài liệu tham khảo](#tài-liệu-tham-khảo)


# 1. Mô hình mạng

![Imgur](https://i.imgur.com/CualjCH.png)

<h3> IP Planning: </h3>

![Imgur](https://i.imgur.com/IVmEum8.png)

# 2. Centos 7

- Cài đặt kho lưu trữ Zabbix:
```
rpm -Uvh https://repo.zabbix.com/zabbix/6.0/rhel/7/x86_64/zabbix-release-6.0-1.el7.noarch.rpm
yum clean all
```
- Cài đặt Agent:
```
yum install -y zabbix-agent
```

- Start Agent:
```
systemctl restart zabbix-agent
systemctl enable zabbix-agent
```

- Cấu hình file: `/etc/zabbix/zabbix_agentd.conf`
```
sudo vi /etc/zabbix/zabbix_agentd.conf
```
- Sửa dòng 117:
```
Server=192.168.77.130
```
- Sửa dòng 164:
```
ServerActive=192.168.77.130
```
- Sửa dòng 175:
```
Hostname=Node01
```

- Trong đó:
  - `Server`: Bật chế độ Check Passive ở Agent
  - `ServerActive`: Bật chế độ Check Active ở Agent
  - `Hostname`:

- Khởi động lại Zabbix Agent:
```
sudo systemctl restart zabbix_agent
```

3. Thêm host giám sát trên Zabbix server:
> Truy cập web server zabbix:

- Đăng nhập vào trang web quản trị zabbix bằng user Admin. 

![Imgur](https://i.imgur.com/5wEuwIp.png)

- Chọn tab `Configuration`> `Hosts` tab> và chọn `Create host`:

![Imgur](https://i.imgur.com/RPgUZXA.png)

- Nhập Host name, Visible name và chọn Templates phù hợp:

![Imgur](https://i.imgur.com/Cin4BuJ.png)

- Chọn Select:

![Imgur](https://i.imgur.com/MkQoMem.png)

- Chọn Openrating systems:

![Imgur](https://i.imgur.com/EGQSx0K.png)

- Sau khi chọn Template, Group thích hợp. Tiếp tục điền Interface:

![Imgur](https://i.imgur.com/GDiXuvE.png)

- Chọn Agent:

![Imgur](https://i.imgur.com/QfCd2Q5.png)

- Nhập thông tin Agent (IP máy cần giám sát), xong chọn `Add`:

![Imgur](https://i.imgur.com/YCqiuu8.png)

- Add thành công:

![Imgur](https://i.imgur.com/xLb4jIB.png)

> Bổ sung cài đặt Agent trên Ubuntu 20.04
- Cài đặt repo zabbix:
```
wget https://repo.zabbix.com/zabbix/6.0/ubuntu/pool/main/z/zabbix-release/zabbix-release_6.0-1+ubuntu20.04_all.deb
sudo dpkg -i zabbix-release_6.0-1+ubuntu20.04_all.deb
sudo apt -y update
```
- Cài đặt Agent:
```
sudo apt install -y zabbix-agent
```
- Start Agent:
```
Sudo systemctl restart zabbix-agent
Sudo systemctl enable zabbix-agent
```




# Tài liệu tham khảo

1. https://www.server-world.info/en/note?os=Ubuntu_20.04&p=zabbix50&f=1
2. https://www.zabbix.com/documentation/6.0/en/manual/installation/frontend
3. https://www.server-world.info/en/note?os=Ubuntu_20.04&p=zabbix50&f=2
4. https://www.zabbix.com/download?zabbix=6.0&os_distribution=ubuntu&os_version=20.04_focal&db=mysql&ws=apache
5. [Install mariadb 10.5](https://mariadb.com/docs/deploy/topologies/single-node/community-server-10-5/)
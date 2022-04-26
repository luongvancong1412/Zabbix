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
Hostname=Node02_centos7
```

- Trong đó:
  - `Server`: Bật chế độ Check Passive ở Agent
  - `ServerActive`: Bật chế độ Check Active ở Agent
  - `Hostname`:

- Khởi động lại Zabbix Agent:
```
sudo systemctl restart zabbix_agent
```
- Mở port:
```
firewall-cmd --zone=public --add-port=10050/tcp --permanent
firewall-cmd --reload
```
3. Thêm host giám sát trên Zabbix server:
> Truy cập web server zabbix:

- Đăng nhập vào trang web quản trị zabbix bằng user Admin. 

![Imgur](https://i.imgur.com/5wEuwIp.png)

- Chọn tab `Configuration`> `Hosts` tab> và chọn `Create host`:

![Imgur](https://i.imgur.com/RPgUZXA.png)

- Nhập Host name, Visible name và chọn Templates phù hợp. Nhập thông tin Agent (IP máy cần giám sát), xong chọn `Add`:

![Imgur](https://i.imgur.com/XZ27b1j.png)





- Add thành công:

![Imgur](https://i.imgur.com/tgjXilS.png)


# Tài liệu tham khảo

1. https://www.zabbix.com/download?zabbix=6.0&os_distribution=centos&os_version=7&db=&ws=
2. https://www.server-world.info/en/note?os=Ubuntu_20.04&p=zabbix50&f=7
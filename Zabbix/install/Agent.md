<h1> Install Agent </h1>


<h2> Mục lục </h2>

- [Centos 7](#centos-7)
- [Ubuntu 18.04](#ubuntu-1804)
- [Ubuntu 20.04](#ubuntu-2004)
- [Tài liệu tham khảo](#tài-liệu-tham-khảo)

# Centos 7

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

# Ubuntu 18.04

- Cài đặt kho lưu trữ zabbix:
```
wget https://repo.zabbix.com/zabbix/6.0/ubuntu/pool/main/z/zabbix-release/zabbix-release_6.0-1+ubuntu18.04_all.deb
sudo dpkg -i zabbix-release_6.0-1+ubuntu18.04_all.deb
sudo apt update -y
```
- Cài đặt Agent:
```
sudo apt install -y zabbix-agent
```
- Start Agent:
```
sudo systemctl restart zabbix-agent
sudo systemctl enable zabbix-agent
```

# Ubuntu 20.04
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

1. https://www.zabbix.com/download
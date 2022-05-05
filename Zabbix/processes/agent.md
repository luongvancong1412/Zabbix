<h1> Agent </h1>

---
<h2> item lục </h2>

- [1. Tổng quan](#1-tổng-quan)
- [2. Check passive và check active](#2-check-passive-và-check-active)
- [3. Nền tảng hỗ trợ](#3-nền-tảng-hỗ-trợ)
- [4. Agent trên các hệ thống UNIX-like](#4-agent-trên-các-hệ-thống-unix-like)
  - [4.1 Cài đặt](#41-cài-đặt)
  - [4.2 Quản lý Agent](#42-quản-lý-agent)
    - [4.2.1 Nếu được cài đặt dưới dạng gói](#421-nếu-được-cài-đặt-dưới-dạng-gói)
    - [4.2.2 Khởi động thủ công](#422-khởi-động-thủ-công)
- [5. Agent trên hệ thống Windows](#5-agent-trên-hệ-thống-windows)
  - [5.1 Chuẩn bị](#51-chuẩn-bị)
  - [5.2 Cài đặt](#52-cài-đặt)
- [6 Các option Agent khác](#6-các-option-agent-khác)
- [7. Kiểm soát thời gian chạy](#7-kiểm-soát-thời-gian-chạy)
- [8. Các loại quy trình Agent](#8-các-loại-quy-trình-agent)
- [9. Process user](#9-process-user)
- [10. Ngôn ngữ](#10-ngôn-ngữ)
- [11. Mã thoát](#11-mã-thoát)
- [Tài liệu tham khảo](#tài-liệu-tham-khảo)
---
# 1. Tổng quan
- `Agent Zabbix` được triển khai trên `thiết bị giám sát` để chủ động `giám sát các tài nguyên` và `ứng dụng cục bộ` (ổ cứng, bộ nhớ, thống kê bộ xử lý, v.v.).

- Trong trường hợp có lỗi , host Zabbix có thể chủ động cảnh báo cho quản trị viên của máy cụ thể đã báo cáo lỗi.

- Các Agent Zabbix cực kỳ hiệu quả vì sử dụng các lệnh gọi hệ thống tự nhiên (native system calls) để thu thập thông tin thống kê.
- Sử dụng tốt trên các máy tính có tài nguyên thấp

# 2. Check passive và check active

- Các Agent Zabbix có thể thực hiện check: `passive` và `active`.

![Imgur](https://i.imgur.com/PCKG48A.png)

- Trong check passive , Server Zabbix (hoặc proxy) yêu cầu dữ liệu, Agent phản hồi lại yêu cầu dữ liệu đó.

- Check active phức tạp hơn. Trước tiên, nhân viên truy xuất danh sách các `item` từ host Zabbix để xử lý. Sau đó, nó sẽ định kỳ gửi các giá trị mới đến server.

- Việc kiểm tra passive hay active đượ cấu hình bằng cách chọn loại item giám sát:
  - *Zabbix agent* - Nếu check passive
  - *Zabbix agent (active)* - Nếu check active

<h3> List of checks được Agent hỗ trợ</h3>

**Network**
- Packets/bytes transferred (*Các gói/byte được chuyển*)
- Errors/dropped packets (*Gói bị lỗi/Xoá*)
- Collisions (*Xung đột*)

**CPU**
- Load average (Tải trung bình)
- CPU idle/usage (CPU nhàn rỗi/sử dụng)
- CPU utilization data per individual process (Dữ liệu CPU sử dụng cho mỗi process)

**Memory**	
- Free/used memory (Bộ nhớ trống/đã sử dụng)
- Swap/pagefile utilization (Sử dụng Hoán đổi/tệp trang)

**Disk**	
- Space free/used (Dung lượng trống/Đã sử dụng)
- Read and write I/O (Đọc và ghi I/O)

**Service**
- Process status
- Process memory usage
- Service status (ssh, ntp, ldap, smtp, ftp, http, pop, nntp, imap)
- Windows service status
- DNS resolution (Phân giải DNS)
- TCP connectivity (Kết nối TCP)
- TCP response time (Thời gian phản hồi)

**File**
- File size/time (Kích thước/Thời gian tệp)
- File exists (File tồn tại)
- Checksum
- MD5 hash (băm MD5)
- RegExp search

**Log**
- Text log (Nhật ký văn bản)
- Windows eventlog (Nhật ký sự kiện windows)

**Other**
- System uptime (Thời gian hoạt động hệ thống)
- System time (Giờ hệ thống)
- Users connected (Người dùng đã kết nối)
- Performance counter (Windows) - Bộ đếm hiệu suất

# 3. Nền tảng hỗ trợ
- Linux
- AIX của IBM
- FreeBSD
- NetBSD
- OpenBSD
- HP-UX
- Mac OS X
- Solaris: 9, 10, 11
- Windows: tất cả các phiên bản desktop và server kể từ bản XP

![Imgur](https://i.imgur.com/kQoDA3p.png)
# 4. Agent trên các hệ thống UNIX-like
- Agent trên các hệ thống giống UNIX được chạy trên server đang được giám sát.

## 4.1 Cài đặt
Xem phần cài đặt gói để biết hướng dẫn về cách cài đặt Zabbix agent dưới dạng gói.

Ngoài ra, hãy xem hướng dẫn cài đặt thủ công nếu bạn không muốn sử dụng các gói.

## 4.2 Quản lý Agent
### 4.2.1 Nếu được cài đặt dưới dạng gói
- Khởi động Agent trên hầu hết các hệ thống GNU/Linux bằng cách thực thi:
```
shell> service zabbix-agent start
```
- Trên các hệ thống khác, bạn có thể cần chạy:
```
shell> /etc/init.d/zabbix-agent start
```
- Để dừng/ khởi động lại/ xem trạng thái của Agent Zabbix, có thể sử dụng các lệnh sau:
```
shell> service zabbix-agent stop
shell> service zabbix-agent restart
shell> service zabbix-agent status
```

### 4.2.2 Khởi động thủ công
- Nếu cách trên không hoạt động, phải khởi động nó theo cách thủ công. Tìm đường dẫn đến tệp nhị phân zabbix_agentd và thực hiện:
```
shell> zabbix_agentd
```
# 5. Agent trên hệ thống Windows
- Agent Zabbix trên Windows chạy dưới dạng dịch vụ Windows.

## 5.1 Chuẩn bị
- Agent Zabbix được phân phối dưới dạng một kho lưu trữ zip (a zip archive).
- Sau khi tải xuống bản lưu trữ, cần giải nén nó. Chọn bất kỳ thư item nào để lưu trữ Agent Zabbix và tệp configuration, ví dụ:
```
C:\zabbix
```
- Sao chép tệp `bin\zabbix_agentd.exe` và `conf\zabbix_agentd.conf` vào `c:\zabbix`.

- Chỉnh sửa tệp c:\zabbix\zabbix_agentd.conf theo yêu cầu, đảm bảo thông số "Hostname" chính xác.

## 5.2 Cài đặt
Sau khi hoàn tất việc chuẩn bị, sử dụng lệnh sau để cài đặt Zabbix agent dưới dạng dịch vụ Windows:
```
C:\> c:\zabbix\zabbix_agentd.exe -c c:\zabbix\zabbix_agentd.conf -i
```
- Bây giờ sẽ có thể cấu hình dịch vụ "Zabbix agent" bình thường như bất kỳ dịch vụ Windows nào khác.

- [Xem thêm](https://www.zabbix.com/documentation/current/en/manual/appendix/install/windows_agent#installing-agent-as-windows-service) chi tiết về cài đặt và chạy Agent Zabbix trên Windows.

# 6 Các option Agent khác
- Có thể chạy nhiều phiên bản của Agent trên một host.
- Nếu sử dụng một phiên bản duy nhất có thể sử dụng tệp cấu hình mặc định hoặc tệp cấu hình được chỉ định trong dòng lệnh.
- Trong trường hợp có nhiều cá thể, mỗi cá thể Agent phải có tệp cấu hình riêng (một trong các phiên bản đó có thể sử dụng tệp cấu hình mặc định).

Các tham số dòng lệnh sau có thể được sử dụng với Agent Zabbix:

> Agent UNIX và Windows

Tham số|Mô tả tả|
|---|---|
|`-c --config <config-file>`|Đường dẫn đến tệp cấu hình.<br>Sử dụng tùy chọn này để chỉ định tệp cấu hình mà không sử dụng tệp mặc định.<br>Trên UNIX, mặc định là `/usr/local/etc/zabbix_agentd.conf` hoặc được đặt bởi các biến thời gian biên dịch `--sysconfdir` hoặc `--prefix`.<br>Trên Windows, mặc định là `c:\zabbix_agentd.conf`
`-p --print`|	In các item đã biết và thoát.<br>Lưu ý : Để trả về kết quả tham số người dùng , phải chỉ định tệp cấu hình (nếu tệp không nằm ở vị trí mặc định).
`-t --test <item key>`|Kiểm tra item đã chỉ định và thoát.<br>Lưu ý : Để trả về kết quả tham số người dùng , bạn phải chỉ định tệp cấu hình (nếu tệp không nằm ở vị trí mặc định).
`-h --help`|Hiển thị thông tin trợ giúp
`-V --version`|Hiển thị số phiên bản

>Chỉ Agent UNIX

Tham số|Mô tả tả|
|---|---|
`-R --runtime-control <option>`|	Thực hiện các chức năng quản trị. Xem [runtime control]() .

>Chỉ dành cho Agent Windows

Tham số|Mô tả tả|
|---|---|
-m --multiple-agents|Sử dụng nhiều phiên bản Agent(với các hàm -i, -d, -s, -x).<br>dĐể phân biệt tên dịch vụ của các phiên bản, mỗi tên dịch vụ sẽ bao gồm giá trị `Hostname  từ tệp cấu hình được chỉ định.

Chỉ tác Agent Windows (chức năng)

Tham số|Mô tả tả|
|---|---|
-i --install|	Cài đặt Zabbix Windows agent dưới dạng dịch vụ
-d -- uninstall|	Gỡ cài đặt dịch vụ Agent Zabbix Windows
-s --start	|Khởi động dịch vụ Agent Zabbix Windows
-x --stop	|Dừng dịch vụ Agent Zabbix Windows

Ví dụ cụ thể về việc sử dụng các tham số dòng lệnh:

- in tất cả các item Agnet được tích hợp sẵn với các giá trị
- Kiểm tra thông số người dùng với key "mysql.ping" được xác định trong tệp cấu hình được chỉ định
- Cài đặt dịch vụ "Zabbix Agent" cho Windows bằng đường dẫn mặc định đến tệp cấu hình `c:\zabbix_agentd.conf`
- Cài đặt dịch vụ "Zabbix Agent [Hostname]" cho Windows bằng cách sử dụng tệp cấu hình zabbix_agentd.conf nằm trong cùng thư item với tệp thực thi Agent và đặt tên dịch vụ duy nhất bằng cách mở rộng nó theo giá trị Hostname từ tệp cấu hình.
```
shell> zabbix_agentd --print
shell> zabbix_agentd -t "mysql.ping" -c /etc/zabbix/zabbix_agentd.conf
shell> zabbix_agentd.exe -i
shell> zabbix_agentd.exe -i -m -c zabbix_agentd.conf
```
# 7. Kiểm soát thời gian chạy
Với các tùy chọn Runtime control, bạn có thể thay đổi cấp độ nhật ký của các quy trình Agent.

Option|	Mô tả|	item tiêu
|---|---|---|
`log_level_increase [= <target>]`	|Tăng cấp độ nhật ký.<br>Nếu item tiêu không được chỉ định, tất cả các quá trình sẽ bị ảnh hưởng.	|item tiêu có thể được chỉ định là:<br>Loại quy trình - tất cả các quy trình thuộc loại được chỉ định (ví dụ: trình nghe).<br>loại quy trình, N - loại quy trình và số (ví dụ: bộ nghe, 3) <br>pid - số nhận dạng quy trình (1 đến 65535). Đối với các giá trị lớn hơn, hãy chỉ định item tiêu là 'process-type, N'.
`log_level_decrease [= <target>]`|	Giảm cấp độ nhật ký.<br>Nếu item tiêu không được chỉ định, tất cả các quá trình sẽ bị ảnh hưởng.
`userparameter_reload`	|Tải lại thông số người dùng từ tệp cấu hình hiện tại.<br> Lưu ý rằng UserParameter là tùy chọn cấu hình Agent duy nhất sẽ được tải lại.|

Ví dụ:

- tăng mức độ nhật ký của tất cả các quy trình
- tăng cấp độ nhật ký của quá trình nghe thứ ba
- tăng mức độ nhật ký của quá trình với PID 1234
- giảm mức độ nhật ký của tất cả các quy trình kiểm tra active
```
shell> zabbix_agentd -R log_level_increase
shell> zabbix_agentd -R log_level_increase=listener,3
shell> zabbix_agentd -R log_level_increase=1234
shell> zabbix_agentd -R log_level_decrease="active checks"
```
> Runtime control không được hỗ trợ trên OpenBSD, NetBSD và Windows.

# 8. Các loại quy trình Agent
- active checks- quy trình thực hiện kiểm tra hoạt động
- collector- quy trình thu thập dữ liệu
- listener- quy trình nghe kiểm tra thụ động

Tệp log Agent có thể được sử dụng để quan sát các loại quy trình này.

- Một Zabbix agent chạy trong Linux: `ps u -C zabbix_agentd`

![Imgur](https://i.imgur.com/E4pfm1E.png)

# 9. Process user 
- Có thể chạy Agent với tư cách là bất kỳ người dùng không phải root nào mà không gặp bất kỳ vấn đề nào.
- Vì Agent Zabbix trên UNIX được thiết kế để chạy với tư cách người dùng không phải root.
- Nếu bạn cố gắng chạy nó dưới dạng 'root', nó sẽ chuyển sang người dùng 'zabbix' được mã hóa cứng, người dùng này phải có trên hệ thống của bạn.g
- Chỉ có thể chạy Agent với tư cách 'root' nếu sửa đổi tham số 'AllowRoot' trong file config Agent.


# 10. Ngôn ngữ
- Agent yêu cầu ngôn ngữ UTF-8 để một số item văn bản Agent có thể trả về nội dung như mong muống. 
- Hầu hết các hệ thống Unix-like hiện đại đều có ngôn ngữ UTF-8 làm mặc định. Tuy nhiên, có một số hệ thống có thể cần phải cài đặt.

# 11. Mã thoát
- Trước phiên bản 2.2 Zabbix agent trả về 0 trong trường hợp thoát thành công và 255 trong trường hợp thất bại. 
- Bắt đầu từ phiên bản 2.2 trở lên, Zabbix agent trả về 0 trong trường hợp thoát thành công và 1 trong trường hợp thất bại.

# Tài liệu tham khảo

1. https://www.zabbix.com/documentation/current/en/manual/concepts/agent
2. https://www.zabbix.com/zabbix_agent
<h1> Host and Host group</h1>

<h2> Mục lục</h2>


- [I. Host](#i-host)
  - [1. Cấu hình một host](#1-cấu-hình-một-host)
    - [1.1 Tổng quan](#11-tổng-quan)
  - [2. Cấu hình](#2-cấu-hình)
    - [2.1Tab Host](#21tab-host)
    - [2.2 Tab IPMI](#22-tab-ipmi)
    - [2.3 Tab Tags](#23-tab-tags)
    - [2.4 Tab Macros](#24-tab-macros)
    - [2.5 Tab Host inventory](#25-tab-host-inventory)
    - [2.5 Encryption - Mã hóa</h3>](#25-encryption---mã-hóah3)
- [Tạo host group](#tạo-host-group)
- [Tài liệu tham khảo](#tài-liệu-tham-khảo)


# I. Host

- Zabbix host là thiết bị muốn giám sát bao gồm servers, máy trạm (workstations) , switches,...

- Tạo host là một trong những công việc đầu tiên trong zabbix.
- Host được tổ chức thành các nhóm gọi là host groups

## 1. Cấu hình một host

### 1.1 Tổng quan
- Các bước cấu hình 1 host trong giao diện người dùng Zabbix (Zabbix frontend):
  - Click: `Configuration` → `Hosts` hoặc `Monitoring` → `Hosts`
  - Click vào Create host ở bên phải (hoặc vào host name để chỉnh sửa host hiện có)
  - Nhập các thông số của host trong mẫu

- Có thể sử dụng các nút Clone và Full clone ở Form host hiện có (existing host) để tạo một host mới.
  - Click vào Clone sẽ giữ lại tất cả các thông số của host và template linkage - liên kết mẫu (giữ tất cả các thực thể khỏi các mẫu đó). 
  - Full cũng sẽ giữ lại các thực thể được đính kèm trực tiếp (applications, items, triggers, graphs, low-level discovery rules và web scenarios - kịch bản web).

>Lưu ý : Khi một host được clone, nó sẽ giữ lại tất cả các thực thể mẫu như ban đầu của chúng trên mẫu. 
>Bất kỳ thay đổi nào đối với các thực thể đó được thực hiện ở cấp host hiện có (chẳng hạn như khoảng thời gian item đã thay đổi, biểu thức chính quy được sửa đổi hoặc các nguyên mẫu được thêm vào quy tắc khám phá cấp thấp) sẽ không được sao chép sang host mới; thay vào đó chúng sẽ giống như trên mẫu.

## 2. Cấu hình

Tab host chứa các thuộc tính chung của host :

<p align="center">
<img src=https://i.imgur.com/s0N3IBB.png>
</p>


Tất cả các trường bắt buộc được đánh dấu bằng dấu hoa thị `*` màu đỏ.

### 2.1Tab Host

STT|Tham số <br>Parameter|Mô tả|
|:---:|:---:|---|
1|`Host name`	|Nhập tên host duy nhất. <br>Cho phép sử dụng chữ và số, dấu cách, dấu chấm, dấu gạch ngang và dấu gạch dưới. Tuy nhiên, dấu cách ở đầu và cuối không được phép.<br>Lưu ý: Với Agent Zabbix, tham số tệp cấu hình Agent hostname phải có cùng giá trị với tên host được nhập ở đây.|
2|`Visible name`|	Nhập tên hiển thị duy nhất cho host.<br>Tên này sẽ hiển thị trong danh sách, bản đồ, v.v. thay vì tên host kỹ thuật(có hỗ trợ UTF-8).
3|`Templates`|	Liên kết các mẫu có sẵn với host.<br>Tất cả các thực thể (item, trigger, đồ thị, v.v.) sẽ được kế thừa từ mẫu.<br>Để liên kết một template mới, Nhập tên mẫu vào trường 4|`Link new template`. Một danh sách các mẫu phù hợp sẽ xuất hiện; cuộn xuống để chọn.<br>Các mẫu được chọn trong trường  sẽ được liên kết với host khi biểu mẫu cấu hình host được lưu hoặc cập nhật.<br>Để hủy liên kết một mẫu, hãy sử dụng một trong hai tùy chọn trong khối `Linked templates`:<br>*Unlink*- hủy liên kết mẫu, nhưng giữ nguyên các item, trigger và đồ thị.<br>*Unlink and clear* - hủy liên kết mẫu và xóa tất cả các item, trigger và đồ thị.
4|`Groups`|	Chọn nhóm quản lý cho host(host phải thuộc ít nhất một host group).<br>Một nhóm mới có thể được tạo và liên kết với host group bằng cách thêm tên nhóm không tồn tại.|
5|Interfaces|	Các interface được hỗ trợ cho host: Agent , SNMP , JMX và IPMI.<br> Mặc định, không có interface nào được chọn.<br>Để thêm interface mới, nhấp vào Add trong khối interface , chọn loại interface và nhập thông tin IP/ DNS , Connect to và Port.
5.1| IP address|	Địa chỉ IP host (tùy chọn).
5.2|DNS	name|Tên DNS host (tùy chọn).
5.3|Connect to|	Chọn button tương ứng để host Zabbix biết phải sử dụng gì để truy xuất dữ liệu từ các Agent:<br>IP - Kết nối với địa chỉ IP host (thường được sử dụng).<br>DNS - Kết nối với tên DNS host
5.4|Port|	Số cổng TCP/ UDP.<br>Mặc định là: <br>+ 10050 cho Agent Zabbix<br>+ 161 cho SNMP agent<br>+ 12345 cho JMX<br>+ 623 cho IPMI.
5.5|Default| Nút đặt interface mặc định.
6|Description|	Nhập mô tả của host.
7|Monitored by proxy|Chọn nếu proxy zabbix để giám sát các host:<br>+(no proxy) - host được giám sát bằng Zabbix server, không sử dụng proxy<br>+proxy name - host được giám sát bởi proxy Zabbix với tên "proxy name".
8|Enabled|Đã bật. Chọn để kích hoạt giám sát.<br>Nếu không muốn giám sát, bỏ chọn.|

### 2.2 Tab IPMI

Tab IPMI chứa các thuộc tính để quản lý IPMI .

STT|Tham số|Mô tả
1|Authentication algorithm|Thuật toán xác thực.<br>Chọn thuật toán xác thực.
2|Privilege level|Mức đặc quyền.<br>Chọn mức đặc quyền.
3|Username|Tên người dùng để xác thực. User macros có thể được sử dụng.
4|Password|	Mật khẩu để xác thực. User macros có thể được sử dụng.

### 2.3 Tab Tags

Tab Thẻ cho phép xác định các thẻ host-level . Tất cả các problems (vấn đề) của host sẽ được tag (gắn thẻ) với các giá trị được nhập ở tab Tags.


Các thẻ được hỗ trợ:
- User macros
- {INVENTORY.*} macros
- {HOST.HOST}
- {HOST.NAME}
- {HOST.CONN}
- {HOST.DNS}
- {HOST.IP}
- {HOST.PORT} and {HOST.ID} macros

### 2.4 Tab Macros

- Tab Macro cho phép bạn xác định host-level người dùng macro dưới dạng một cặp tên-giá trị.
- Lưu ý: các giá trị macro có thể được giữ dưới dạng: 
  - văn bản thuần túy
  - văn bản bí mật 
  - hoặc bí mật của Vault. 
- Thêm một mô tả cũng được hỗ trợ.



- Có thể xem các macro template-level và global user macros nếu chọn option `Inherited and host macros` . 
  - Tất cả các user macros đã xác định cho host, hiển thị giá trị, origin của chúng.

https://i.imgur.com/MR0xYQ7.png

- Các liên kết đến các template tương ứng và cấu hình global macro được cung cấp;có thể chỉnh sửa template/global macro ở cấp độ host (host level).

### 2.5 Tab Host inventory

- Tab Host inventory cho phép bạn nhập thông tin inventory cho host theo:
  - Manual - cách thủ công. 
  - Automatic - Tự động 
  - Hoặc Disabled - tắt

https://i.imgur.com/EQUi6vd.png

Nếu bật Inventory (Manual hoặc automatic),sẽ xuất hiện một chấm màu xanh lục trên tab.

https://i.imgur.com/APiyYcB.png

### 2.5 Encryption - Mã hóa</h3>

Tab Mã hóa cho phép bạn yêu cầu các kết nối được mã hóa với host.

STT|Parameter|Description|
|:---:|:---:|---|
1|Connections to host|Kết nối với host ...<br>Cách Zabbix server hoặc proxy kết nối với Agent Zabbix trên host: <br>+ no encryption - không mã hóa (mặc định)<br>+ using PSK (pre-shared key - khóa chia sẻ trước)<br>+ hoặc certificate - chứng chỉ.
2|Connections from host|Kết nối từ host ...	<br>Chọn loại kết nối được phép từ host (từ Agent Zabbix và Zabbix sender).<br>Có thể được chọn nhiều loại cùng một lúc (hữu ích cho việc testing và chuyển sang kiểu kết nối khác).<br>Mặc định là "No encryption".
3|Issuer|Tổ chức phát hành chứng chỉ. Chứng chỉ được xác thực lần đầu với CA (Certificate authority - tổ chức phát hành chứng chỉ).<br>Nếu hợp lệ, được ký bởi CA, thì trường Issuer có thể được sử dụng để hạn chế CA được phép(nếu cài đặt Zabbix của bạn sử dụng chứng chỉ từ nhiều CA).<br> Nếu trống thì bất kỳ CA nào cũng được chấp nhận.
4|Subject|Đối tượng được phép của chứng chỉ. Chứng chỉ lần đầu tiên được xác thực với CA.<br>Nếu nó hợp lệ, được ký bởi CA, thì trường Subject có thể được sử dụng để chỉ cho phép một giá trị của chuỗi subject.<br>Nếu trường này trống thì bất kỳ chứng chỉ hợp lệ nào được ký bởi CA đã định cấu hình đều được chấp nhận.
5|PSK identity|Chuỗi nhận dạng khóa được chia sẻ trước.<br>Không đưa thông tin nhạy cảm vào PSK identity, vì nó được truyền không mã hóa qua mạng để thông báo cho người nhận biết sẽ sử dụng PSK.
6|PSK|	Pre-shared key - Khóa chia sẻ trước (chuỗi hex).<br>Độ dài tối đa:<br>512 chữ số hex (256 byte PSK) nếu Zabbix sử dụng thư viện GnuTLS hoặc OpenSSL<br>64 chữ số hex (PSK 32 byte) nếu Zabbix sử dụng thư viện mbed TLS (PolarSSL).<br>Ví dụ: 1f87b595725ac58dd977beef14b97461a7c1045b9a1c963065002c5473194952|

<h3> Value mapping</h3>

Tab Value mapping cho phép định cấu hình biểu diễn giá trị của các item thành các từ ngữ dễ hiểu hơn.

https://i.imgur.com/YqHHDWQ.png

Ví dụ: Trong hình:
- Trạng thái server: Giá trị:
  - = 0 tương đương "xám"
  - = 1 tương đương "xanh lá"
  - `= 2` tương đương "vàng"
  - `>= 3` tương đương với `đỏ` 

- Khi đó, chữ cái sẽ được sử dụng thay vì hiện các số.

https://i.imgur.com/uRe1fmU.png

- Có thể thêm nhiều `Value mapping`.



# Tạo host group

> Chỉ người dùng Super Admin mới có thể tạo host group.

- Cách tạo một nhóm host trong giao diện (frontend) người dùng Zabbix:

- Chọn: Configuration → host groups
- Click vào Create Group ở góc trên bên phải màn hình
- Nhập các thông số của nhóm vào form

https://i.imgur.com/33RG0kt.png

- Các trường bắt buộc được đánh dấu bằng dấu hoa thị màu đỏ.

STT|Tham số|Mô tả
|:---:|---|---|
1|Group name|Nhập tên nhóm host lưu trữ duy nhất.<br>Sử dụng dấu phân tách dấu gạch chéo '/' để tạo một nhóm host lồng nhau, Ví dụ `HaNoi/ThanhTri/Zabbix servers`.<br>Có thể tạo nhóm này ngay cả khi không có nhóm nào trong 2 nhóm host chính (HaNoi/ThanhTri) tồn tại.<br>Việc tạo các nhóm host mẹ này là tùy thuộc vào người dùng (không được tạo tự động).<br>Không được phép sử dụng các dấu `/` ở đầu và sau cùng hoặc nhiều dấu gạch chéo liên tiếp.<br>Nhóm lồng nha được hỗ trợ kể từ Zabbix 3.2.0.
2|Apply permissions and tag filters to all subgroups|Áp dụng quyền và bộ lọc thẻ cho tất cả các nhóm con	|Checkbox chỉ khả dụng cho người dùng Super Admin và chỉ khi chỉnh sửa nhóm host hiện có.<br>Đánh dấu checkbox và nhấp vào Update để áp dụng cùng một cấp permissions/tag filters cho tất cả các nhóm host lồng nhau. Đối với các nhóm người dùng có thể có các quyền khác nhau trên các nhóm host lồng nhau, cấp độ quyền của nhóm host mẹ sẽ được thực thi trên các nhóm lồng nhau.<br>Đây là tùy chọn một lần không được lưu trong cơ sở dữ liệu.<br>Tùy chọn này được hỗ trợ kể từ Zabbix 3.4.0.|



# Tài liệu tham khảo

1. https://www.zabbix.com/documentation/current/en/manual/config/hosts
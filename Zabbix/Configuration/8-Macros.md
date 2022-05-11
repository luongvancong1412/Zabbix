<h1> Macros </h1>

<h2> Mục lục </h2>

- [1.Tổng quan](#1tổng-quan)
- [2. Macro functions](#2-macro-functions)
  - [2.1 Tổng quan](#21-tổng-quan)
  - [2.2 Các macro function được hỗ trợ](#22-các-macro-function-được-hỗ-trợ)
    - [`fmtnum (<digits>)`](#fmtnum-digits)
    - [`fmttime (<format>, <time_shift>)`](#fmttime-format-time_shift)
    - [`iregsub (<pattern>, <output>)`](#iregsub-pattern-output)
    - [`regsub (<pattern>, <output>)`](#regsub-pattern-output)
  - [3. Example](#3-example)
    - [3.1 Làm tròn](#31-làm-tròn)

# 1.Tổng quan
- Zabbix hỗ trợ một số macro mẫu có thể được sử dụng trong các trường hợp khác nhau.
- Các macro là các biến, được xác định bằng cú pháp:
```
{MACRO}
``` 

Lợi ích:
- cho phép tiết kiệm thời gian 
- và làm cho cấu hình Zabbix minh bạch hơn.

- Cách sử dụng điển hình: sử dụng trong một Templates.
- Do đó, một trigger trên một Templates có thể được đặt tên là `Processor load too high on {HOST.NAME}`. 
- Khi áp dụng mẫu này cho host, ví dụ như Zabbix server, tên sẽ được đổi thành `Processor load is too high on Zabbix server` khi `trigger được hiển thị` trong phần `Monitoring`.

- Các Macro có thể được sử dụng trong các tham số của item key. Ví dụ:  `item.key[server_{HOST.HOST}_local]`.

- Các loại macros:
  - `Built-in` (Cài sẵn)
  - `User-defined` (người dùng tự định nghĩa)

Xem thêm:
- Danh sách đầy đủ các [built-in macro](https://www.zabbix.com/documentation/current/en/manual/appendix/macros/supported_by_location)


# 2. Macro functions
## 2.1 Tổng quan
- Các Macro functions cung cấp khả năng tùy chỉnh các giá trị macro .

- Cú pháp của một hàm macro là:
```
{<macro>.<func>(<params>)}
```
Trong đó:

- `<macro>` - Tên biến sử dụng (ví dụ: {ITEM.VALUE} hoặc {#LLDMACRO})
- `<func>` - Hàm áp dụng
- `<params>` - Danh sách các tham số của hàm được phân tách bằng dấu phẩy.

Ví dụ:

- `{{TIME}.fmttime(format,time_shift)}`
- `{{ITEM.VALUE}.regsub(pattern, output)}`
- `{{#LLDMACRO}.regsub(pattern, output)}`


## 2.2 Các macro function được hỗ trợ
### `fmtnum (<digits>)`
|Description|Parameters|Supported for|
|---|---|---|
|Kiểm soát số chữ số được in sau dấu thập phân.|`Digits` (chữ số) - số chữ số sau dấu thập phân.<br> Nếu không có sẽ thêm số `0` sau dấu phẩy|{ITEM.VALUE}<br>{ITEM.LASTVALUE}<br>Expression macros
### `fmttime (<format>, <time_shift>)`
|Description|Parameters|Supported for|
|---|---|---|
|Định dạng thời gian.|	`format` - bắt buộc, tương thích với định dạng `time_shift` của hàm `strftime`.<br>`time_shift`- dịch chuyển thời gian; nên bắt đầu bằng<br>`-<N><time_unit>hoặc +<N><time_unit>` <br>Trong đó:<br>+`N` - số đơn vị thời gian muốn dịch chuyển để cộng hoặc trừ;<br>`time_unit` - `h` (hour - giờ), `d` (day - ngày), `w` (week - tuần), `M` (month - tháng) hoặc `y` (year - năm).<br>Kể từ Zabbix 5.4, tham số time_shift hỗ trợ multi-step time và có thể bao gồm `/<time_unit>` (`/d`- nửa đêm, `/w`- ngày đầu tiên trong tuần (thứ Hai), `/M`- ngày đầu tiên của tháng, v.v.). Ví dụ:<br>`-1w` - chính xác 7 ngày trở lại đây;<br>`-1w/w` - Thứ hai của tuần trước;<br>`-1w/w+1d` - Thứ Ba của tuần trước.<br>`-1M/M` - Ngày đầu tiên của tháng trước<br>Các phép toán thời gian được tính từ `trái sang phải`, `không` có thứ tự `ưu tiên`.<br>Ví dụ: `-1M/d+1h/w` sẽ được phân tích cú pháp như `((-1M/d)+1h)/w`.|	{TIME}

### `iregsub (<pattern>, <output>)`

|Description|Parameters|Supported for|
|---|---|:---:|
Trích xuất chuỗi con bằng một đối sánh biểu thức chính quy (không phân biệt chữ hoa chữ thường).|+ `pattern` (mẫu) - biểu thức chính quy để khớp với<br>+`output` (đầu ra) - các tùy chọn đầu ra. `\1` - `\9` trình giữ chỗ được hỗ trợ để chụp các nhóm. `\0` trả về văn bản phù hợp.	|{ITEM.VALUE}<br>{ITEM.LASTVALUE}<br>[Low-level discoverey macros](https://www.zabbix.com/documentation/current/en/manual/config/macros/lld_macros)

### `regsub (<pattern>, <output>)`
|Description|Parameters|Supported for|
|---|---|:---:|
Trích xuất chuỗi con bằng một đối sánh biểu thức chính quy (không phân biệt chữ hoa chữ thường).|+ `pattern` (mẫu) - biểu thức chính quy để khớp với<br>+`output` (đầu ra) - các tùy chọn đầu ra. `\1` - `\9` trình giữ chỗ được hỗ trợ để chụp các nhóm. `\0` trả về văn bản phù hợp.	|{ITEM.VALUE}<br>{ITEM.LASTVALUE}<br>[Low-level discoverey macros](https://www.zabbix.com/documentation/current/en/manual/config/macros/lld_macros)

## 3. Example

### 3.1 Làm tròn
STT|Received value|Macro|Output|
|:---:|---|---|:---:|
1|24.3413523|{{ITEM.VALUE}.fmtnum(2)}|24.34
2|24.3413523|{{ITEM.VALUE}.fmtnum(0)}|24
3|12:36:01|{{TIME}.fmttime(%B)}|October
4|12:36:01|{{TIME}.fmttime(%d %B,-1M/M)}|1 September
5|123Log line|{{ITEM.VALUE}.regsub(^[0-9]+, Problem)}|Problem
6|123 Log line|{{ITEM.VALUE}.regsub("^([0-9]+)", "Problem")}	|Problem
7|123 Log line|	{{ITEM.VALUE}.regsub("^([0-9]+)", Problem ID: \1)}|Problem ID: 123
Log line	{{ITEM.VALUE}.regsub(".*", "Problem ID: \1")}	'' ID sự cố: ''
MySQL crashed errno 123	{{ITEM.VALUE}.regsub("^(\w+).*?([0-9]+)", " Problem ID: \1_\2 ")}	'' ID sự cố: MySQL_123 ''
123 Log line	{{ITEM.VALUE}.regsub("([1-9]+", "Problem ID: \1")}	*UNKNOWN*(biểu thức chính quy không hợp lệ)
customername_1	{{#IFALIAS}.regsub("(.*)_([0-9]+)", \1)}	customername
customername_1	{{#IFALIAS}.regsub("(.*)_([0-9]+)", \2)}	1
customername_1	{{#IFALIAS}.regsub("(.*)_([0-9]+", \1)}	{{#IFALIAS}.regsub("(.*)_([0-9]+", \1)}(biểu thức chính quy không hợp lệ)
customername_1	{$MACRO:"{{#IFALIAS}.regsub(\"(.*)_([0-9]+)\", \1)}"}	{$MACRO:"customername"}
customername_1	{$MACRO:"{{#IFALIAS}.regsub(\"(.*)_([0-9]+)\", \2)}"}	{$MACRO:"1"}
customername_1	{$MACRO:"{{#IFALIAS}.regsub(\"(.*)_([0-9]+\", \1)}"}	{$MACRO:"{{#M}.regsub(\"(.*)_([0-9]+\", \1)}"}(biểu thức chính quy không hợp lệ)
customername_1	"{$MACRO:\"{{#IFALIAS}.regsub(\\"(.*)_([0-9]+)\\", \1)}\"}"	"{$MACRO:\"customername\"}"
customername_1	"{$MACRO:\"{{#IFALIAS}.regsub(\\"(.*)_([0-9]+)\\", \2)}\"}"	"{$MACRO:\"1\"}")
customername_1	"{$MACRO:\"{{#IFALIAS}.regsub(\\"(.*)_([0-9]+\\", \1)}\"}"	"{$MACRO:\"{{#IFALIAS}.regsub(\\"(.*)_([0-9]+\\", \1)}\"}")(biểu thức chính quy không hợp lệ)



Tổng quat
Các macro của người dùng được hỗ trợ trong Zabbix để có tính linh hoạt cao hơn, ngoài các macro được hỗ trợ bên ngoài.

Macro người dùng có thể được xác định ở cấp độ toàn cầu, mẫu và máy chủ. Các macro này có cú pháp đặc biệt:

{$MACRO}
Zabbix giải quyết các macro theo thứ tự ưu tiên sau:

macro cấp máy chủ (được chọn trước)
macro được xác định cho các mẫu cấp đầu tiên của máy chủ (tức là các mẫu được liên kết trực tiếp với máy chủ), được sắp xếp theo ID mẫu
macro được xác định cho các mẫu cấp hai của máy chủ, được sắp xếp theo ID mẫu
macro được xác định cho các mẫu cấp ba của máy chủ lưu trữ, được sắp xếp theo ID mẫu, v.v.
macro toàn cục (được kiểm tra lần cuối)
Nói cách khác, nếu macro không tồn tại cho một máy chủ, Zabbix sẽ cố gắng tìm nó trong các mẫu máy chủ lưu trữ có độ sâu ngày càng tăng. Nếu vẫn không được tìm thấy, một macro toàn cục sẽ được sử dụng, nếu tồn tại.

 Nếu một macro có cùng tên tồn tại trên nhiều mẫu được liên kết cùng cấp, thì macro từ mẫu có ID thấp nhất sẽ được sử dụng. Do đó, việc có các macro có cùng tên trong nhiều mẫu là một rủi ro về cấu hình.
Nếu Zabbix không thể tìm thấy macro, thì macro đó sẽ không được giải quyết.

 Các macro (bao gồm cả macro của người dùng) không được giải quyết trong phần Cấu hình (ví dụ: trong danh sách trình kích hoạt) theo thiết kế để làm cho cấu hình phức tạp trở nên minh bạch hơn.
Macro người dùng có thể được sử dụng trong:

thông số khóa mục
khoảng thời gian cập nhật mặt hàng và khoảng thời gian linh hoạt
tên và mô tả kích hoạt
các tham số và hằng số biểu thức kích hoạt (xem ví dụ )
nhiều địa điểm khác - xem danh sách đầy đủ
Các trường hợp sử dụng phổ biến của macro máy chủ và toàn cầu
sử dụng macro toàn cục ở một số vị trí; sau đó thay đổi giá trị macro và áp dụng các thay đổi cấu hình cho tất cả các vị trí bằng một cú nhấp chuột
tận dụng lợi thế của các mẫu có thuộc tính dành riêng cho máy chủ: mật khẩu, số cổng, tên tệp, biểu thức chính quy, v.v.
Cấu hình
Để xác định macro người dùng, hãy chuyển đến vị trí tương ứng trong giao diện người dùng:

đối với macro toàn cục, hãy truy cập Quản trị → Chung → Macro
cho macro máy chủ lưu trữ và cấp mẫu, mở thuộc tính máy chủ lưu trữ hoặc mẫu và tìm kiếm tab Macro
 Nếu macro người dùng được sử dụng trong các mục hoặc trình kích hoạt trong mẫu, bạn nên thêm macro đó vào mẫu ngay cả khi nó được xác định ở cấp độ toàn cầu. Bằng cách đó, nếu loại macro là văn bản xuất mẫu sang XML và nhập mẫu đó vào một hệ thống khác sẽ vẫn cho phép nó hoạt động như mong đợi. Giá trị của macro bí mật không được xuất .
Macro người dùng có các thuộc tính sau:



Tham số	Sự miêu tả
Macro	Tên macro. Tên phải được đặt trong dấu ngoặc nhọn và bắt đầu bằng ký hiệu đô la.
Ví dụ: {$ FRONTEND_URL}. Các ký tự sau được phép trong tên macro: AZ (chỉ viết hoa) , 0-9 , _ ,.
Giá trị	Giá trị vĩ mô. Ba loại giá trị được hỗ trợ:
Văn bản (mặc định) - giá trị văn bản thuần túy Văn bản
bí mật - giá trị được che bằng dấu hoa thị, có thể hữu ích để bảo vệ thông tin nhạy cảm như mật khẩu hoặc khóa dùng chung.
Vault secret - giá trị chứa một đường dẫn tham chiếu (như 'path: key', ví dụ: "secret / zabbix: password") đến bí mật của Vault

Lưu ý rằng mặc dù giá trị của macro bí mật bị ẩn khỏi tầm nhìn, nhưng giá trị có thể được tiết lộ thông qua việc sử dụng trong các mặt hàng. Ví dụ: trong một tập lệnh bên ngoài, câu lệnh 'echo' tham chiếu đến macro bí mật có thể được sử dụng để tiết lộ giá trị macro cho giao diện người dùng vì máy chủ Zabbix có quyền truy cập vào giá trị macro thực.

Để chọn loại giá trị, hãy nhấp vào nút ở cuối trường nhập giá trị:
biểu tượng cho biết macro văn bản;
biểu tượng cho biết một macro văn bản bí mật. Khi di chuột, trường giá trị chuyển thành một nút cho phép nhập giá trị mới của macro (để thoát mà không lưu giá trị mới, hãy nhấp vào biểu tượng mũi tên ngược ( ). Biểu thị macro Vault bí mật. Độ dài tối đa của macro người dùng giá trị là 2048 ký tự (255 ký tự trong các phiên bản trước 5.2.0).


Sự miêu tả	Trường văn bản được sử dụng để cung cấp thêm thông tin về macro này.
 Các URL chứa macro bí mật sẽ không hoạt động vì macro trong đó sẽ được phân giải thành "******".
 Trong biểu thức kích hoạt, macro người dùng sẽ giải quyết nếu tham chiếu đến một tham số hoặc hằng số. Chúng sẽ KHÔNG giải quyết nếu tham chiếu đến máy chủ lưu trữ, khóa mục, chức năng, toán tử hoặc một biểu thức kích hoạt khác. Không thể sử dụng macro bí mật trong biểu thức kích hoạt.
Các ví dụ
ví dụ 1
Sử dụng macro cấp máy chủ trong khóa mục "Trạng thái của daemon SSH":

net.tcp.service[ssh,,{$SSH_PORT}]

Mục này có thể được chỉ định cho nhiều máy chủ, miễn là giá trị của {$ SSH_PORT} được xác định trên các máy chủ đó.

Ví dụ 2
Sử dụng macro cấp máy chủ trong trình kích hoạt "CPU tải quá cao":

last(/ca_001/system.cpu.load[,avg1])>{$MAX_CPULOAD}

Trình kích hoạt như vậy sẽ được tạo trên mẫu, không được chỉnh sửa trong các máy chủ riêng lẻ.

 Nếu bạn muốn sử dụng số lượng giá trị làm tham số hàm (ví dụ: max (/ host / key, # 3) ), hãy bao gồm dấu thăng trong định nghĩa macro như sau: SOME_PERIOD => # 3
Ví dụ 3
Sử dụng hai macro trong trình kích hoạt "CPU tải quá cao":

min(/ca_001/system.cpu.load[,avg1],{$CPULOAD_PERIOD})>{$MAX_CPULOAD}

Lưu ý rằng một macro có thể được sử dụng như một tham số của hàm kích hoạt, trong ví dụ này là hàm min () .

Ví dụ 4
Đồng bộ hóa điều kiện không có sẵn của tác nhân với khoảng thời gian cập nhật mặt hàng:

xác định macro {$ INTERVAL} và sử dụng nó trong khoảng thời gian cập nhật mặt hàng;
sử dụng {$ INTERVAL} làm tham số của trình kích hoạt tính không khả dụng của tác nhân:
nodata(/ca_001/agent.ping,{$INTERVAL})=1

Ví dụ 5
Tập trung cấu hình giờ làm việc:

tạo macro {$ WORKING_HOURS} toàn cục bằng 1-5,09:00-18:00;
sử dụng nó trong trường Thời gian làm việc trong Quản trị → Chung → GUI ;
sử dụng nó trong trường Khi hoạt động trong Quản trị → Người dùng → Phương tiện ;
sử dụng nó để thiết lập thăm dò mục thường xuyên hơn trong giờ làm việc:


sử dụng nó trong điều kiện Hành động khoảng thời gian ;
điều chỉnh thời gian làm việc trong Quản trị → Chung → Macro , nếu cần.
Ví dụ 6
Sử dụng macro nguyên mẫu máy chủ để định cấu hình các mục cho các máy chủ đã phát hiện:

trên một nguyên mẫu máy chủ, hãy xác định macro người dùng {$ SNMPVALUE} với macro khám phá cấp thấp {#SNMPVALUE} dưới dạng giá trị:


gán mẫu SNMPv2 Chung cho nguyên mẫu máy chủ;
sử dụng {$ SNMPVALUE} trong trường SNMP OID của các mục mẫu SNMPv2 Chung .
Ngữ cảnh macro người dùng
Xem macro của người dùng với ngữ cảnh .


3 macro người dùng với ngữ cảnh
Tổng quat
Một ngữ cảnh tùy chọn có thể được sử dụng trong macro người dùng , cho phép ghi đè giá trị mặc định bằng một ngữ cảnh cụ thể.

Ngữ cảnh được thêm vào tên macro; cú pháp phụ thuộc vào việc ngữ cảnh có phải là giá trị văn bản tĩnh hay không:

{$MACRO:"static text"}
hoặc một biểu thức chính quy:

{$MACRO:regex:"regular expression"} 
Lưu ý rằng chỉ có thể xác định macro với ngữ cảnh biểu thức chính quy trong cấu hình macro người dùng. Nếu regex:tiền tố được sử dụng ở nơi khác làm ngữ cảnh macro người dùng, như trong biểu thức trình kích hoạt, nó sẽ được coi là ngữ cảnh tĩnh.

Trích dẫn ngữ cảnh là tùy chọn (xem thêm các ghi chú quan trọng ).

Ví dụ về ngữ cảnh macro:

Ví dụ	Sự miêu tả
{$LOW_SPACE_LIMIT}	Macro người dùng không có ngữ cảnh.
{$LOW_SPACE_LIMIT:/tmp}	Macro người dùng với ngữ cảnh (chuỗi tĩnh).
{$LOW_SPACE_LIMIT:regex:"^/tmp$"}	Macro người dùng với ngữ cảnh (biểu thức chính quy). Giống như {$LOW_SPACE_LIMIT:/tmp}.
{$LOW_SPACE_LIMIT:regex:"^/var/log/.*$"}	Macro người dùng với ngữ cảnh (biểu thức chính quy). Đối sánh tất cả các chuỗi có tiền tố là / var / log /.
Trường hợp sử dụng
Macro người dùng với ngữ cảnh có thể được xác định để đạt được các ngưỡng linh hoạt hơn trong biểu thức kích hoạt (dựa trên các giá trị được truy xuất bởi khám phá cấp thấp). Ví dụ: bạn có thể xác định các macro sau:

{$ LOW_SPACE_LIMIT} = 10
{$ LOW_SPACE_LIMIT: / home} = 20
{$ LOW_SPACE_LIMIT: regex: "^ \ / [az] + $"} = 30
Sau đó, macro khám phá cấp thấp có thể được sử dụng làm ngữ cảnh macro trong nguyên mẫu kích hoạt để khám phá hệ thống tệp được gắn kết:

last(/host/vfs.fs.size[{#FSNAME},pfree])<{$LOW_SPACE_LIMIT:"{#FSNAME}"}
Sau khi phát hiện, các ngưỡng không gian thấp khác nhau sẽ được áp dụng trong trình kích hoạt tùy thuộc vào các điểm gắn kết được phát hiện hoặc loại hệ thống tệp. Sự kiện sự cố sẽ được tạo ra nếu:

/ home folder có ít hơn 20% dung lượng ổ đĩa trống
các thư mục khớp với mẫu regexp (như / etc, / tmp hoặc / var) có ít hơn 30% dung lượng đĩa trống
các thư mục không khớp với mẫu regexp và không phải / home có ít hơn 10% dung lượng đĩa trống
Ghi chú quan trọng
Nếu tồn tại nhiều macro người dùng với ngữ cảnh, trước tiên Zabbix sẽ cố gắng đối sánh macro ngữ cảnh đơn giản và sau đó đối sánh macro ngữ cảnh với biểu thức chính quy theo một thứ tự không xác định.
 Không tạo các macro ngữ cảnh khác nhau khớp với cùng một chuỗi để tránh hành vi không xác định.
Nếu một macro có ngữ cảnh không được tìm thấy trên máy chủ lưu trữ, các mẫu được liên kết hoặc trên toàn cầu, thì macro không có ngữ cảnh sẽ được tìm kiếm.
Chỉ các macro khám phá cấp thấp mới được hỗ trợ trong ngữ cảnh. Bất kỳ macro nào khác đều bị bỏ qua và được coi là văn bản thuần túy.
Về mặt kỹ thuật, ngữ cảnh macro được chỉ định bằng cách sử dụng các quy tắc tương tự như các tham số chính của mục , ngoại trừ ngữ cảnh macro không được phân tích cú pháp thành một số tham số nếu có ,ký tự:

Ngữ cảnh macro phải được trích dẫn "nếu ngữ cảnh có chứa }ký tự hoặc bắt đầu bằng "ký tự. Trích dẫn bên trong ngữ cảnh được trích dẫn phải được thoát cùng với \ký tự.
Bản \thân ký tự không được thoát, có nghĩa là không thể có ngữ cảnh được trích dẫn kết thúc bằng \ký tự - macro {$ MACRO: "a: \ b \ c \"} không hợp lệ.
Các dấu cách đầu tiên trong ngữ cảnh bị bỏ qua, các dấu cách ở cuối thì không:
Ví dụ: {$ MACRO: A} giống với {$ MACRO: A}, nhưng không giống với {$ MACRO: A}.
Tất cả các khoảng trắng trước dấu ngoặc kép đầu và sau dấu ngoặc kép đều bị bỏ qua, nhưng tất cả các khoảng trắng bên trong dấu ngoặc kép thì không:
Các macro {$ MACRO: "A"}, {$ MACRO: "A"}, {$ MACRO: "A"} và {$ MACRO: "A"} giống nhau, nhưng macro {$ MACRO: "A"} và {$ MACRO: "A"} thì không.
Tất cả các macro sau đều tương đương vì chúng có cùng ngữ cảnh: {$ MACRO: A}, {$ MACRO: A} và {$ MACRO: "A"}. Điều này trái ngược với các khóa mục, trong đó 'key [a]', 'key [a]' và 'key ["a"]' giống nhau về mặt ngữ nghĩa, nhưng khác nhau vì mục đích duy nhất.


4 macro khám phá cấp độ thấp
Tổng quat
Có một loại macro được sử dụng trong hàm khám phá cấp thấp (LLD):

{#MACRO} 
Nó là một macro được sử dụng trong quy tắc LLD và trả về các giá trị thực của tên hệ thống tệp, giao diện mạng, SNMP OID, v.v.

Các macro này có thể được sử dụng để tạo nguyên mẫu mục, trình kích hoạt và biểu đồ . Sau đó, khi khám phá hệ thống tệp thực, giao diện mạng, v.v., các macro này được thay thế bằng các giá trị thực và là cơ sở để tạo các mục, trình kích hoạt và đồ thị thực.

Các macro này cũng được sử dụng để tạo nguyên mẫu máy chủ và nhóm máy chủ trong khám phá máy ảo .

Một số macro khám phá cấp thấp được "đóng gói sẵn" với hàm LLD trong Zabbix - {#FSNAME}, {#FSTYPE}, {#IFNAME}, {#SNMPINDEX}, {#SNMPVALUE}. Tuy nhiên, việc tuân theo những tên này là không bắt buộc khi tạo quy tắc khám phá cấp thấp tùy chỉnh . Sau đó, bạn có thể sử dụng bất kỳ tên macro LLD nào khác và tham chiếu đến tên đó.

Các địa điểm được hỗ trợ
Các macro LLD có thể được sử dụng:

trong bộ lọc quy tắc khám phá cấp thấp
cho các nguyên mẫu vật phẩm trong
Tên
các thông số quan trọng
đơn vị
cập nhật khoảng 1
lịch sử lưu trữ thời kỳ 1
thời gian lưu trữ xu hướng 1
các bước xử lý trước giá trị mặt hàng
SNMP OID
Trường cảm biến IPMI
công thức mục được tính toán
Tập lệnh SSH và tập lệnh Telnet
giám sát cơ sở dữ liệu truy vấn SQL
Trường điểm cuối mục JMX
sự miêu tả
Trường URL tác nhân HTTP
Trường tác nhân HTTP Trường truy vấn HTTP
Trường nội dung yêu cầu tác nhân HTTP
Trường mã trạng thái bắt buộc của tác nhân HTTP
Khóa và giá trị của trường tiêu đề tác nhân HTTP
Trường tên người dùng xác thực HTTP tác nhân HTTP
Tác nhân HTTP Trường mật khẩu xác thực HTTP
Trường proxy HTTP tác nhân HTTP
Tác nhân HTTP Trường tệp chứng chỉ SSL HTTP
Tác nhân HTTP Trường tệp khóa HTTP SSL
Tác nhân HTTP Trường mật khẩu khóa SSL HTTP
Trường thời gian chờ của tác nhân HTTP 1
thẻ
cho các nguyên mẫu kích hoạt trong
Tên
Dữ liệu hoạt động
biểu thức (chỉ trong hằng số và tham số hàm)
URL
sự miêu tả
thẻ
cho các nguyên mẫu biểu đồ trong
Tên
cho các nguyên mẫu máy chủ trong
Tên
tên hiển thị
các trường giao diện tùy chỉnh: IP, DNS, cổng, cộng đồng SNMP v1 / v2, tên ngữ cảnh SNMP v3, tên bảo mật SNMP v3, cụm mật khẩu xác thực SNMP v3, cụm mật khẩu bảo mật SNMP v3
tên nguyên mẫu của nhóm máy chủ
giá trị thẻ máy chủ
giá trị macro máy chủ
(xem danh sách đầy đủ )
Ở tất cả những nơi đó, macro LLD có thể được sử dụng bên trong ngữ cảnh macro người dùng tĩnh .

Sử dụng các hàm macro
Các hàm macro được hỗ trợ với macro khám phá cấp thấp (ngoại trừ trong bộ lọc quy tắc khám phá cấp thấp), cho phép trích xuất một phần nhất định của giá trị macro bằng cách sử dụng biểu thức chính quy.

Ví dụ: bạn có thể muốn trích xuất tên khách hàng và số giao diện từ macro LLD sau cho mục đích gắn thẻ sự kiện:

{#IFALIAS}=customername_1
Để làm như vậy, regsubhàm macro có thể được sử dụng với macro trong trường giá trị thẻ sự kiện của nguyên mẫu trình kích hoạt:



Lưu ý rằng không được phép sử dụng dấu phẩy trong các tham số khóa của mục chưa được trích dẫn , vì vậy tham số chứa hàm macro phải được trích dẫn. Ký tự dấu gạch chéo ngược ( \) nên được sử dụng để thoát khỏi dấu ngoặc kép bên trong tham số. Ví dụ:

net.if.in["{{#IFALIAS}.regsub(\"(.*)_([0-9]+)\", \1)}",bytes]
Để biết thêm thông tin về cú pháp hàm macro, hãy xem: Hàm macro

Các chức năng macro được hỗ trợ trong macro khám phá cấp thấp kể từ Zabbix 4.0.

Chú thích
1 Trong các trường được đánh dấu bằng 1 , một macro duy nhất phải điền vào toàn bộ trường. Nhiều macro trong một trường hoặc macro trộn với văn bản không được hỗ trợ.



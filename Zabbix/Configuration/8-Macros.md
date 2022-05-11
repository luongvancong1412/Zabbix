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
    - [3.2 Tính toán thời gian](#32-tính-toán-thời-gian)
    - [3.3 Regsub](#33-regsub)

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
1|24.3413523|`{{ITEM.VALUE}.fmtnum(2)}`|24.34
2|24.3413523|`{{ITEM.VALUE}.fmtnum(0)}`|24

### 3.2 Tính toán thời gian
STT|Received value|Macro|Output|
|:---:|---|---|:---:|
1|12:36:01|`{{TIME}.fmttime(%B)}`|October
2|12:36:01|`{{TIME}.fmttime(%d %B,-1M/M)}`|1 September

### 3.3 Regsub
STT|Received value|Macro|Output|
|:---:|---|---|:---:|
1|123Log line|`{{ITEM.VALUE}.regsub(^[0-9]+, Problem)}`|Problem
2|123 Log line|`{{ITEM.VALUE}.regsub("^([0-9]+)", "Problem")}`|Problem
3|123 Log line|`{{ITEM.VALUE}.regsub("^([0-9]+)", Problem ID: \1)}`|Problem ID: 123
4|Log line|`{{ITEM.VALUE}.regsub(".*", "Problem ID: \1")}`|" Problem ID:"
5|MySQL crashed errno 123|`{{ITEM.VALUE}.regsub("^(\w+).*?([0-9]+)", " Problem ID: \1_\2 ")}`|"Problem ID: MySQL_123"
6|123 Log line|`{{ITEM.VALUE}.regsub("([1-9]+", "Problem ID: \1")}`|`*UNKNOWN*`(invalid regular expression - biểu thức chính quy không hợp lệ)
|customername_1|`{{#IFALIAS}.regsub("(.*)_([0-9]+)", \1)}`|customername
7|customername_1|`{{#IFALIAS}.regsub("(.*)_([0-9]+)", \2)}`|1
customername_1|`{{#IFALIAS}.regsub("(.*)_([0-9]+", \1)}`|`{{#IFALIAS}.regsub("(.*)_([0-9]+", \1)}`(invalid regular expression)





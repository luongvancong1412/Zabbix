<h1> Regular expressions </h1>

<h2> Mục lục </h2>

- [1. Tổng quan](#1-tổng-quan)
- [2. Biểu thức chính quy](#2-biểu-thức-chính-quy)
- [3. Biểu thức chính quy toàn cục](#3-biểu-thức-chính-quy-toàn-cục)
    - [Tab Expression](#tab-expression)
    - [Tab Test](#tab-test)
- [4. Biểu thức chính quy chung mặc định](#4-biểu-thức-chính-quy-chung-mặc-định)
- [5. Ví dụ](#5-ví-dụ)
  - [Ví dụ 1](#ví-dụ-1)
  - [Ví dụ với công cụ sửa đổi regex nội tuyến](#ví-dụ-với-công-cụ-sửa-đổi-regex-nội-tuyến)
  - [Một ví dụ khác với công cụ sửa đổi regex nội tuyến](#một-ví-dụ-khác-với-công-cụ-sửa-đổi-regex-nội-tuyến)
- [Tài liệu tham khảo](#tài-liệu-tham-khảo)



# 1. Tổng quan

- Có hai cách sử dụng biểu thức chính quy trong Zabbix:
  - Nhập biểu thức chính quy theo cách thủ công (`manually`)
  - Bằng cách sử dụng một `global regular expression` (biểu thức chính quy toàn cục) được tạo trong Zabbix

# 2. Biểu thức chính quy
- Có thể nhập biểu thức chính quy theo cách thủ công vào những vị trí được hỗ trợ. Lưu ý: biểu thức có thể không bắt đầu bằng `@` vì ký hiệu đó được sử dụng trong Zabbix để tham chiếu các `global regular expression`.

- Lưu ý rằng trong multi-line matching, ký tự `^`và `$` tương ứng lần lượt ở đầu/cuối mỗi dòng, thay vì đầu/cuối của toàn bộ chuỗi.

# 3. Biểu thức chính quy toàn cục
- Có một `avanced editor` (trình chỉnh sửa nâng cao) để tạo và kiểm tra các biểu thức chính quy phức tạp trong giao diện người dùng Zabbix (`frontend Zabbix`).

-Sử dụng `@` để tham chiếu đến tên của `global regular expression`, ví dụ: `@mycustomregexp` .

- Tạo một `global regular expression`:
  - Chọn: `Administration` → `General`
  - Click `Regular expression` từ menu thả xuống
  
    ![Imgur](https://i.imgur.com/eCAHF3J.png)

  - Click vào `New regular expression`
  
    ![Imgur](https://i.imgur.com/eoMiTr4.png)

### Tab Expression
- Cho phép đặt tên biểu thức chính quy và thêm biểu thức phụ.

![Imgur](https://i.imgur.com/Qqq0kjD.png)

STT|Parameter|Mô tả|
|:---:|---|---|
1|`Name`|	Đặt tên biểu thức chính quy. All ký tự Unicode nào đều được phép.
2|`Expressions`|Click vào `Add` trong `Expressions` block để thêm một biểu thức con mới.
2.1|`Expression type`|Chọn kiểu biểu thức:<br>+ `Character string included` - tương ứng với chuỗi con<br>+ `Any character string included` - khớp với bất kỳ chuỗi con nào từ danh sách được phân cách. Danh sách được phân tách bao gồm dấu phẩy (,), dấu chấm (.) Hoặc dấu gạch chéo (/).<br>+ `Character string not included` - khớp với bất kỳ chuỗi nào ngoại trừ chuỗi con<br>+ `Result is TRUE` - khớp với biểu thức chính quy<br>+ `Result is FALSE` - không khớp với biểu thức chính quy
2.2|`Expression`|	Nhập chuỗi con/biểu thức chính quy.
3|`Delimiter`<br>(Dấu phân cách)|	Dấu phẩy (,), dấu chấm (.) Hoặc dấu gạch chéo lên (/) để phân tách các chuỗi văn bản trong một biểu thức chính quy.<br>Tham số này chỉ khả dụng khi Expression type là Any character string included.
4|`Case sensitive`|Checkbox chỉ định xem một biểu thức chính quy có nhạy cảm với việc viết hoa các chữ cái hay không.

### Tab Test
- Biểu thức chính quy và biểu thức con của nó có thể được kiểm tra bằng cách cung cấp một chuỗi kiểm tra (`test string`).

![Imgur](https://i.imgur.com/TBssIzt.png)

- Kết quả: hiển thị trạng thái của từng biểu thức con và tổng trạng thái biểu thức tùy chỉnh.

![Imgur](https://i.imgur.com/FlCN3kS.png)

- Tổng trạng thái biểu thức tùy chỉnh được xác định là Kết quả kết hợp (`Combined result`).
- Zabbix sử dụng toán tử logic `AND` để tính toán kết quả `Combined result` (Nếu một kết quả là `False` thì `Combined result` cũng có trạng thái `False`).

# 4. Biểu thức chính quy chung mặc định

![Imgur](https://i.imgur.com/ZfcyMAb.png)

STT|Name|Expression|Matches|
|---|---|---|---|
1|File systems for discovery|`^(btrfs\|ext2\|ext3\|ext4\|jfs\|reiser\|xfs\|ffs\|ufs\|jfs\|jfs2\|vxfs\|hfs\|refs\|apfs\|ntfs\|fat32\|zfs)$`|`btrfs` hoặc `ext2` hoặc "`ext3`" hoặc "`ext4`" hoặc "`jfs"` hoặc "`reiser`" hoặc "`xfs`" hoặc "`ffs`" hoặc "`ufs`" hoặc "`jfs`" hoặc "`jfs2`" hoặc "`vxfs`" hoặc "`hfs` "hoặc" `refs` "hoặc" `apfs` "hoặc" `ntfs` "hoặc" `fat32` "hoặc" `zfs` "
2|Network interface for discovery|^Software Loopback Interface|Chuỗi bắt đầu bằng `Software Loopback Interface`.
3||`^lo$`	|"lo"
4||`^(In)?[Ll]oop[Bb]ack[0-9._]*$`	|Các chuỗi tùy chọn bắt đầu bằng "`In`", sau đó có "`L`" hoặc "`l`", sau đó "`oop`", sau đó "`B`" hoặc "`b`", sau đó "`ack`", có thể được tùy chọn theo sau bởi bất kỳ số chữ số, dấu chấm `.` hoặc gạch dưới `_`.
5||`^NULL[0-9.]*$`|Các chuỗi bắt đầu bằng "`NULL`" tùy ý theo sau bởi bất kỳ số chữ số hoặc dấu chấm nào.
6||`^[Ll]o[0-9.]*$`|	Các chuỗi bắt đầu bằng "`Lo`" hoặc "`lo`" và được theo sau bởi bất kỳ số chữ số hoặc dấu chấm nào.
7||`^[Ss]ystem$`	|"`System`" hoặc "`system`"
8||`^Nu[0-9.]*$`|Các chuỗi bắt đầu bằng "`Nu`" tùy ý theo sau bởi bất kỳ số chữ số hoặc dấu chấm nào.
9|Storage devices for SNMP discovery|	`^(Physical memory\|Virtual memory\|Memory buffers\|Cached memory\|Swap space)$`|	"`Physical memory`" or "`Virtual memory`" or "`Memory buffers`" or "`Cached memory`" or "`Swap space`"
10|Windows service names for discovery|	`^(MMCSS\|gupdate\|SysmonLog\|clr_optimization_v2.0.50727_32\|clr_optimization_v4.0.30319_32)$`	|"`MMCSS`" hoặc "`gupdate`" hoặc "`SysmonLog`" hoặc các chuỗi như "`clr_optimization_v2.0.50727_32`" và "`clr_optimization_v4.0.30319_32`" trong đó thay vì dấu chấm, bạn có thể đặt bất kỳ ký tự nào ngoại trừ dòng mới.
11|Windows service startup states for discovery|`^(automatic\|automatic delayed)$`	|"automatic" or "automatic delayed"

# 5. Ví dụ

## Ví dụ 1
Sử dụng biểu thức sau trong low-level discovery để khám phá cơ sở dữ liệu ngoại trừ cơ sở dữ liệu có tên cụ thể:
- Kiểm tra CSDL có trùng với tên `TESTDATABASE` không:
```
^TESTDATABASE$
```

![Imgur](https://i.imgur.com/ut4NkRK.png)

- Đã chọn Expression type: "Result is FALSE". Không khớp với tên, chứa chuỗi " TESTDATABASE ".

## Ví dụ với công cụ sửa đổi regex nội tuyến
- Sử dụng biểu thức chính quy sau bao gồm một công cụ sửa đổi nội dòng (?i) để khớp với các ký tự "error":
```
(?i)error
```
- Test: Các chuỗi có từ `error`:

![Imgur](https://i.imgur.com/2uptfTM.png)

- Đã chọn Expression type: "Result is FALSE".. Các ký tự "lỗi" được khớp.

## Một ví dụ khác với công cụ sửa đổi regex nội tuyến
- Sử dụng biểu thức chính quy sau bao gồm nhiều công cụ sửa đổi trong dòng để khớp các ký tự sau một dòng cụ thể:
```
(?<=match (?i)everything(?-i) after this line\n)(?sx).*# we add s modifier to allow . match newline characters
```
![Imgur](https://i.imgur.com/3hg9mPQ.png)




Đã chọn Expression type: "Result is TRUE". Các ký tự sau một dòng cụ thể được khớp.

![Imgur](https://i.imgur.com/qiv6LwZ.png)

> Danh sách các công cụ sửa đổi có sẵn có thể được tìm thấy trong [trang pcresyntax](https://www.pcre.org/original/doc/html/pcrepattern.html).
> Để biết thêm thông tin về cú pháp PCRE, vui lòng tham khảo tài liệu [PCRE HTML](https://www.pcre.org/original/doc/html/pcresyntax.html#SEC16) .


# Tài liệu tham khảo

1. https://www.zabbix.com/documentation/current/en/manual/regular_expressions
<h1> Templates </h1>

<h2>Mục lục</h2>

- [1. Tổng quan](#1-tổng-quan)
- [2. Configuration 1 template](#2-configuration-1-template)
  - [2.1 Tổng quan](#21-tổng-quan)
  - [2.2 Creating a template](#22-creating-a-template)
    - [Tab Templates](#tab-templates)
      - [Thuộc tính template](#thuộc-tính-template)
    - [Tab Thẻ](#tab-thẻ)
    - [Tab Macros](#tab-macros)
    - [Tab Value mapping](#tab-value-mapping)
  - [2.3 Thêm các item, trigger, graph](#23-thêm-các-item-trigger-graph)
  - [2.4 Adding dashboards](#24-adding-dashboards)
  - [2.5 Adding web scenarios](#25-adding-web-scenarios)
- [3. Liên kết/Huỷ liên kết](#3-liên-kếthuỷ-liên-kết)
  - [3.1 Linking](#31-linking)
  - [3.2 Liên kết một template](#32-liên-kết-một-template)
  - [3.3 Tính duy nhất của thực thể](#33-tính-duy-nhất-của-thực-thể)
  - [3.4 Hủy liên kết một template](#34-hủy-liên-kết-một-template)
- [4. Nesting](#4-nesting)
- [5. Mass update (Cập nhật hàng loạt)](#5-mass-update-cập-nhật-hàng-loạt)
- [Tài liệu tham khảo](#tài-liệu-tham-khảo)

# 1. Tổng quan
- **`Templates` là một tập hợp các entity có thể được áp dụng nhanh cho nhiều host.**

- Entities có thể là:
  - `items`
  - `triggers`
  - `graphs`
  - `dashboards`
  - `low-level discovery rules`
  - `web scenarios`

- Trên thực tế có nhiều **host cấu hình giống nhau**, với các template, ta có thể sao chép chúng vào một Templates và sau đó **áp dụng Templates cho nhiều host** nếu cần.

- Khi một template được liên kết với host, **tất cả các thực thể (items, triggers, graphs,...)** của template sẽ được **thêm vào host.**
- **Các template được chỉ định** trực tiếp cho **từng host riêng lẻ** (chứ không phải cho một nhóm host).

- Các template thường được sử dụng để nhóm các thực thể cho các dịch vụ hoặc ứng dụng cụ thể (như Apache, MySQL, PostgreSQL, Postfix...) và sau đó áp dụng cho các host chạy các dịch vụ đó.

- Ngoài ra, khi cần thay đổi 1 cái gì đó trong các host. Configuration template từ một lần sẽ truyền thay đổi đến tất cả các host được liên kết.

**Do đó, Sử dụng các template là một cách để giảm khối lượng công việc của một người và giúp hợp lý hóa cấu hình Zabbix.**

# 2. Configuration 1 template

## 2.1 Tổng quan
Việc định cấu hình một template:
- yêu cầu **trước tiên** bạn phải **tạo một template** bằng cách xác định các thông số chung của nó
- sau đó thêm các thực thể (**item, trigger, graph, v.v.**) vào nó.

## 2.2 Creating a template
Để tạo một template:

- Đi tới `Configuration → Templates`

  ![Imgur](https://i.imgur.com/iGswvbJ.png)

- Click vào `Create template`

  ![Imgur](https://i.imgur.com/wGWVHMC.png)

- Chỉnh sửa thuộc tính của `template`

  ![Imgur](https://i.imgur.com/aToHDnl.png)

### Tab Templates
- Chứa các thuộc tính template chung.

![Imgur](https://i.imgur.com/aToHDnl.png)

- Tất cả các trường bắt buộc được đánh dấu bằng dấu hoa thị `*` màu đỏ.

#### Thuộc tính template

- **Template name:**
  - Tên của Template phải là duy nhất.
  - Cho phép sử dụng `chữ` và `số`, `dấu cách`, `dấu chấm`, `dấu gạch ngang` và `dấu gạch dưới`. 
  - Không được sử dụng `dấu cách` ở đầu và cuối.
- Visible name:
  - 	Tên hiển thị của `template` trong các list, maps, v.v.

- **Templates:**
  - Link `một hoặc nhiều` template `nested` (lồng nhau) với `template` này. Tất cả `entities`  (items, triggers, graphs, v.v.) được `kế thừa` từ các `template được link`.
  - Để link một template mới, Cần nhập tên template vào trường `Link new templates` . Một list các template liên quan sẽ xuất hiện; cuộn xuống để chọn. 
  - Ngoài ra, bạn có thể click vào `Select` bên cạnh trường và chọn các `template` từ list trong cửa sổ bật lên. Các template được chọn trong trường `Link new templates` sẽ được liên kết với template cấu hình template được save hoặc Update.
  - Để unlink một template, có thể sử dụng một trong hai tùy chọn trong khối `Linked templates` :
    - `Unlink`- `hủy liên kết` template, nhưng `giữ nguyên` các item, trigger và graph của nó.
    - `Unlink and clear` - `hủy liên kết` template và `xóa tất cả` các item, trigger và graph của nó
- **Groups:** template thuộc về Nhóm host hoặc nhóm template.
- **Description:**	Nhập mô tả template.


### Tab Thẻ 
- cho phép bạn xác định các `template-level tag` . 
- Tất cả các `Problem` của host được liên kết với template này sẽ `được gắn thẻ` với các giá trị được nhập tại đây.

![Imgur](https://i.imgur.com/6N0PmJ8.png)

- Usesr Macros, macro {INVENTORY. *}, {HOST.HOST}, {HOST.NAME}, {HOST.CONN}, {HOST.DNS}, {HOST.IP}, {HOST.PORT} và {HOST.ID } macro được hỗ trợ trong `Tags`.

### Tab Macros
- Cho phép xác định template-level user macros dưới dạng một cặp `name-value`. 

![Imgur](https://i.imgur.com/kMoRp98.png)

- Lưu ý: các giá trị macro có thể được giữ dưới dạng plain text, secret text, or Vault secret.
- **Description:** nhập mô tả

### Tab Value mapping
- cho phép định cấu hình biểu diễn thân thiện với con người của dữ liệu item trong ánh xạ giá trị .

![Imgur](https://i.imgur.com/WjTV3Id.png)

Nút:

![Imgur](https://i.imgur.com/KS1vhC7.png)
STT|Button|Description|
|:---: |:---:|---|
1|![Imgur](https://i.imgur.com/jdo36fc.png)|Thêm template. Mẫu được thêm vào sẽ xuất hiện trong `list`.
2|![Imgur](https://i.imgur.com/P0l7AMY.png) |Câp nhật các thuộc tính của một template hiện có.
3|![Imgur](https://i.imgur.com/TsEr4HA.png)	|**Tạo một template khác** dựa trên các thuộc tính của template hiện tại, bao gồm các thực thể (item, trigger, v.v.) được **kế thừa** từ các template được liên kết.
4|![Imgur](https://i.imgur.com/UlUCoby.png)	|Tạo một template khác dựa trên các thuộc tính của template hiện tại, bao gồm các thực thể (item, trigger, v.v.) cả hai đều được kế thừa từ các template được liên kết và được gắn trực tiếp vào template hiện tại.
5|![Imgur](https://i.imgur.com/4JwhXE8.png)	|Xóa template; các thực thể của template (item, trigger, v.v.) vẫn còn với các host được liên kết.
6	|![Imgur](https://i.imgur.com/A7UbdSr.png)|Xóa template và tất cả các thực thể của nó khỏi các host được liên kết.
7	|![Imgur](https://i.imgur.com/rX3cg9F.png)|Hủy chỉnh sửa các thuộc tính template.
Với một template đã tạo, tiếp theo tiến hành thêm một số entity vào đó.

>Các item phải được thêm vào một template trước. 
>Không thể thêm trigger và graph nếu không có item tương ứng.
## 2.3 Thêm các item, trigger, graph
Để thêm các item vào template:
- Đi tới `Configuration → Host` (hoặc `Templates` )
- Click vào Các `item` trong hàng của host / template được yêu cầu
  ![Imgur](https://i.imgur.com/YGrMDGJ.png)
- Đánh dấu các checkbox của các item bạn muốn thêm vào template
- Click vào `Copy` bên dưới danh sách item

  ![Imgur](https://i.imgur.com/F3z7XvC.png)
- Chọn template (hoặc nhóm template) mà các item sẽ được sao chép vào và click vào Sao chép

Thêm trigger và biểu đồ được thực hiện theo cách tương tự (từ danh sách trigger và biểu đồ tương ứng).

## 2.4 Adding dashboards

Để thêm trang tổng quan vào một template trong` Configuration` → `Templates`

- Click vào `Dashboards` trong hàng của template
- Configure dashboard theo các guideline của [Configuring dashboards](https://www.zabbix.com/documentation/current/en/manual/web_interface/frontend_sections/monitoring/dashboard)
 
>Các tiện ích con có thể được đưa vào trang tổng quan template là: classic graph, graph prototype, clock, plain text, URL.
 
 
 >Để biết chi tiết về cách truy cập trang tổng quan host được tạo từ trang tổng quan template, hãy xem phần   [host dashboard ](https://www.zabbix.com/documentation/current/en/manual/config/visualization/host_screens#accessing-host-dashboards)

## 2.5 Adding web scenarios
Để thêm các kịch bản web vào một template trong `Configuration` → `Templates`
- Click vào `Web` trong hàng của `template`
- [Configure web scenarios](https://www.zabbix.com/documentation/current/en/manual/web_monitoring#configuring-a-web-scenario)

# 3. Liên kết/Huỷ liên kết

## 3.1 Linking
- `Linking` là một quá trình theo đó các template được áp dụng cho các host
- `Unlinking` sẽ loại bỏ sự liên kết với template khỏi host.

## 3.2 Liên kết một template
- Để Link một template với host:

  - Đi tới `Congfiguration → Hosts`
  - Click vào `host` được yêu cầu
  - Bắt đầu nhập tên template vào trường Templates . Một danh sách các template phù hợp sẽ xuất hiện; cuộn xuống để chọn.
    ![Imgur](https://i.imgur.com/JdQAvl7.png)
  - Ngoài ra, bạn có thể click vào Chọn bên cạnh trường và chọn một hoặc một số template từ danh sách trong cửa sổ bật lên
  - Click vào `Add`/ `Update` trong biểu template thuộc tính host
    ![Imgur](https://i.imgur.com/CH0jTHX.png)

- Host bây giờ sẽ có tất cả các thực thể (items, triggers, graphs..) của template.

- Khi các thực thể (items, triggers, graphs etc.) được thêm vào từ template:
  - các thực thể giống hệt nhau hiện có trước đây trên host được cập nhật dưới dạng các thực thể của template
  - các thực thể từ template được thêm vào
  - bất kỳ thực thể được liên kết trực tiếp nào, trước liên kết template, chỉ tồn tại trên host vẫn không bị ảnh hưởng

- Trong danh sách, tất cả các thực thể từ template bây giờ đều có tiền tố là tên template, cho biết rằng chúng thuộc về template cụ thể. Bản thân tên template (bằng văn bản màu xám) là một liên kết cho phép truy cập danh sách các thực thể đó ở cấp template.

Nếu một thực thể nào đó (item, trigger, biểu đồ, v.v.) không có tiền tố là tên template, điều đó có nghĩa là nó đã tồn tại trên host trước đó và không được template thêm vào.

## 3.3 Tính duy nhất của thực thể
- Khi thêm các thực thể vào template, phải biết những thực thể nào đã tồn tại trên host, cần được cập nhật và những thực thể nào khác nhau. 
- Các tiêu chí về tính duy nhất để quyết định sự giống nhau/ khác biệt là:
  - for items - the item key
  - for triggers - trigger name and expression
  - for custom graphs - graph name and its items

## 3.4 Hủy liên kết một template
- Để hủy liên kết một template khỏi host:
  - Đi tới `Configuration → Hosts`
  - Click vào host được yêu cầu và tìm trường Templates
  - Click vào `Unlink` hoặc `Unlink and clear` bên cạnh template để hủy liên kết
    ![Imgur](https://i.imgur.com/YHJha5Z.png)
    
  - Click vào `Update` để hoàn thành

# 4. Nesting
- Nesting (Lồng nhau) là liên kết một số mẫu với 1 mẫu hiện tại.
- Lợi ích: Chỉ cần liên kết 1 mẫu với một host. Host sẽ tự động kế thừa (`inherit`) tất cả các `entities` của các mẫu được liên kết.
# 5. Mass update (Cập nhật hàng loạt)
- Khi muốn thay đổi một số thuộc tính cho một số Template cùng 1 lúc, ta có thể sử dụng chức năng `Mass update` để làm việc đó.

<h3> Các bước thực hiện</h3>

- Chọn các `templates` muốn `Update` trong `Templates list` bằng cách tích vào `checkbox` của template đó.
  ![Imgur](https://i.imgur.com/Si8mnYy.png)
- Click vào `Mass update` bên dưới list
- Di chuyển đến `tab` có các thuộc tính bắt buộc (templates, Tags, Macros, hoặc Value mapping)
  ![Imgur](https://i.imgur.com/yRFvws4.png)
- Tích vào `checkbox` của t`huộc tính muốn update` và nhập giá trị mới.
  ![Imgur](https://i.imgur.com/mG7tb8x.png)

# Tài liệu tham khảo

1. https://www.zabbix.com/documentation/current/en/manual/config/templates
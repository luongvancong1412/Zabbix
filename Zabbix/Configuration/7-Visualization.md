<h1> Visualization </h1>

<h2> item lục </h2>

- [1. Graphs](#1-graphs)
  - [1.1 Tổng quan](#11-tổng-quan)
  - [1.2 Simple graphs](#12-simple-graphs)
    - [1.2.1 Tổng quan](#121-tổng-quan)
    - [1.2.2 Time period selector (Kiểm soát thời gian)](#122-time-period-selector-kiểm-soát-thời-gian)
    - [1.2.3 Dữ liệu gần đây và dữ liệu so với khoảng thời gian lâu hơn](#123-dữ-liệu-gần-đây-và-dữ-liệu-so-với-khoảng-thời-gian-lâu-hơn)
    - [1.2.4 Trigger lines](#124-trigger-lines)
- [Tài liệu tham khảo](#tài-liệu-tham-khảo)

# 1. Graphs
## 1.1 Tổng quan
- Sẽ trở nên **dễ dàng hơn** nếu người dùng có thể **nhìn vào đồ thị trực quan** về những gì đang diễn ra (Dữ liệu thu thập đư) **thay vì** chỉ có **những con số**.

![Imgur](https://i.imgur.com/pj823Lp.png)

- Đồ thị cho phép **nắm bắt nhanh** luồng dữ liệu (`data flow`), tương quan các vấn đề (`correlate problems`), khám phá (`discover`) khi nào điều gì đó **bắt đầu** hoặc thời điểm điều gì đó có thể biến thành **PROBLEM**.

- Zabbix cung cấp cho người dùng:

  - Đồ thị đơn giản [(simple graphs)](https://www.zabbix.com/documentation/current/en/manual/config/visualization/graphs/simple) được tích hợp sẵn (`built-in`) của dữ liệu một `item`
  - Khả năng **tạo các biểu đồ tùy chỉnh** [(customized graphs)](https://www.zabbix.com/documentation/current/en/manual/config/visualization/graphs/custom) phức tạp hơn
  - Truy cập vào so sánh một số `item` một cách nhanh chóng trong [biểu đồ đặc biệt](https://www.zabbix.com/documentation/current/en/manual/config/visualization/graphs/adhoc)
  - Đồ thị vector [(vector graphs)](https://www.zabbix.com/documentation/current/en/manual/web_interface/frontend_sections/monitoring/dashboard/widgets#graph) hiện đại có thể tùy chỉnh

## 1.2 Simple graphs
### 1.2.1 Tổng quan
- Mục đích: **trực quan hóa dữ liệu** được thu thập bởi các item.

- Được cung cấp miễn phí bởi Zabbix:
  - Chọn :`Monitoring → Latest data` và click vào liên kết `Graphs` cho item tương ứng và một **biểu đồ** sẽ **được hiển thị**.
    ![Imgur](https://i.imgur.com/cnU7Sxg.png)
 
### 1.2.2 Time period selector (Kiểm soát thời gian)
- Nó cho phép `chọn các khoảng thời gian` bằng một `cú click chuột`.

> Note:
> - Các option như `Today`, `This week`, `This month`, `This year` hiển thị **toàn bộ khoảng thời gian**, bao gồm cả giờ/ngày trong tương lai.
> - Ngược lại, `Today` chỉ hiển thị **số giờ** đã trôi qua.

- Có thể được di chuyển qua lại trong thời gian bằng cách click vào các nút mũi tên.
    ![Imgur](https://i.imgur.com/FpS9DSK.png)
-  Nút Thu nhỏ cho phép thu nhỏ khoảng thời gian `2 lần` hoặc `50% theo mỗi hướng`. Cũng có thể thu nhỏ bằng cách **click đúp vào biểu đồ**.

- Các trường `From/To` hiển thị khoảng thời gian đã chọn trong:

  - Cú pháp **thời gian tuyệt đối**:`Y-m-d H:i:s`
    ![Imgur](https://i.imgur.com/EAsez6H.png)
  - Cú pháp **thời gian tương đối**, ví dụ:`now-1d-25m+50s`
    ![Imgur](https://i.imgur.com/A8NCx9r.png)


- Ở **định dạng tương đối** có thể sử dụng phép toán (`-` hoặc `+`)
- Ví dụ: `now-1d` hoặc `now-1d-2h+5m`. 
- Các ký hiệu được hỗ trợ ở định dạng tương đối:
  - `Now`
  - `s` (seconds)
  - `m` (minutes)
  - `h` (hours)
  - `d` (days)
  - `w` (weeks)
  - `M` (months)
  - `y` (years)

- Có thể chọn **1 ngày bắt đầu/kết thúc** **cụ thể** bằng cách click vào biểu tượng lịch bên cạnh các trường `From/To` .

![Imgur](https://i.imgur.com/SoctamI.png)


- Cách khác, **chọn một khu vực trong biểu đồ bằng nút chuột trái**. Biểu đồ sẽ phóng to vào vùng được đánh dấu sau khi thả nút chuột trái.


### 1.2.3 Dữ liệu gần đây và dữ liệu so với khoảng thời gian lâu hơn
- Đối với **dữ liệu rất gần đây**, **một đường thẳng** được vẽ **nối mỗi giá trị** nhận được.

- Đối với dữ liệu cũ hơn, ba đường được vẽ 
  - 1 đường màu **xanh lá cây đậm** hiển thị giá trị **trung bình**
  - 1 đường **màu hồng nhạt** hiển thị các giá trị **lớn nhất** tại từng thời điểm
  - 1 đường **màu xanh lục nhạt** hiển thị các giá trị **nhỏ nhất** tại thời điểm đó. 
  - Khoảng trống giữa mức cao và mức thấp: tô bằng **nền màu vàng**.

- **Thời gian làm việc** (ngày làm việc) được hiển thị trong biểu đồ dưới dạng **nền trắng**
- **Thời gian không làm việc** được hiển thị bằng **màu xám** (với chủ đề giao diện người dùng mặc định màu xanh gốc ).

- Thời gian làm việc **không hiển thị** nếu biểu đồ hiển thị **thời gian > 3 tháng**.

### 1.2.4 Trigger lines

# Tài liệu tham khảo

1. 
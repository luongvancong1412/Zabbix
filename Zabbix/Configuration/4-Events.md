<h1> Events </h1>

<h2> Mục lục </h2>

- [1. Tổng quan](#1-tổng-quan)
- [2. Tạo Trigger event](#2-tạo-trigger-event)
  - [2.1 Tổng quan](#21-tổng-quan)
  - [2.2 Problem event](#22-problem-event)
  - [2.2 OK event](#22-ok-event)
  - [2.3 Triggers](#23-triggers)
  - [2.4 Event correlation](#24-event-correlation)
  - [2.5 Task manager](#25-task-manager)
- [3 Nguồn event khác](#3-nguồn-event-khác)
  - [3.1 Service events](#31-service-events)
  - [3.2 Discovery events](#32-discovery-events)
  - [3.3 Event tự động phát hiện Agent đang hoạt động](#33-event-tự-động-phát-hiện-agent-đang-hoạt-động)
  - [3.3 Internall events](#33-internall-events)
- [4 Đóng thủ công các PROBLEM](#4-đóng-thủ-công-các-problem)
  - [4.1 Tổng quan](#41-tổng-quan)
  - [4.2 Cấu hình](#42-cấu-hình)
    - [4.2.1 Trigger configuration](#421-trigger-configuration)
    - [4.2.2 Problem update window](#422-problem-update-window)
    - [4.3 Xác minh](#43-xác-minh)
- [Tài liệu tham khảo](#tài-liệu-tham-khảo)

# 1. Tổng quan

Các loại events trong Zabbix:

- `Trigger events` - khi một trigger thay đổi trạng thái của nó(`OK` → `PROBLEM` → `OK`).
- `Service events` - khi một dịch vụ thay đổi trạng thái của nó (`OK` → `PROBLEM` → `OK`).
- `Discovery events` - khi host hoặc dịch vụ được phát hiện (tìm thấy)
- `Autoregistration events` - khi các active Agent được server đăng ký tự động (auto-registered)
- `Internal events` - khi một item/low-level discovery rule không được hỗ trợ hoặc trigger chuyển sang trạng thái `Unknown`.

> Các internal event được hỗ trợ bắt đầu từ phiên bản Zabbix 2.2.
- Các event được đánh dấu thời gian (time-stamped)

Để xem chi tiết các event, chọn: `Monitoring → Problem`.


# 2. Tạo Trigger event
## 2.1 Tổng quan
- Event thường xuyên nhất, quan trọng nhất: `Sự thay đổi trạng thái của Trigger`.

- Mỗi khi `Trigger thay đổi trạng thái` của nó, một `event sẽ được tạo ra`. 
  - Chứa thông tin chi tiết về sự thay đổi của trạng thái trigger - thời gian xảy ra và trạng thái mới là gì.

- Trigger tạo ra 2 loại event - `Problem` và `OK`.

## 2.2 Problem event
- Problem event được tạo:

  - Khi một biểu thức Trigger đánh giá là `TRUE` nếu Trigger ở trạng thái OK;
  - Mỗi khi một biểu thức Trigger đánh giá là `TRUE` nếu quá trình multiple problem event được bật cho Trigger.
## 2.2 OK event
Một OK event closes (các) event Problem liên quan và có thể được tạo bởi 3 thành phần:

- Trigger - dựa trên cài đặt 'OK event generation' và 'OK event closes';
- Event correlation - tương quan sự kiện
- Task manager (trình quản lý tác vụ) - khi một event được đóng theo cách thủ công.
## 2.3 Triggers
Trigger có cài đặt 'OK event generation'  để kiểm soát cách tạo event OK:

- Expression (Biểu thức) - một event OK được tạo từ một Trigger ở trạng thái có PROBLEM khi Biểu thức đánh giá là FALSE (bật theo mặc định).
- Recovery expression - một event OK xuất hiện từ một Trigger ở trạng thái có Problem khi 
  - biểu thức của nó đánh giá là FALSE 
  - và biểu thức khôi phục đánh giá là TRUE. 
Điều này có thể được sử dụng nếu tiêu chí khôi phục Trigger khác với tiêu chí Problem.

- None - Một Event OK không bao giờ được tạo ra. Điều này có thể được sử dụng kết hợp với nhiều event tạo Problem để chỉ cần gửi thông báo khi có điều gì đó xảy ra.

Ngoài ra, Trigger có cài đặt `OK event closes` kiểm soát event `Problem` nào được đóng:

- `All problems` - một OK event sẽ đóng tất cả các Problem mở được tạo bởi Trigger
- `All problems if tag values match` - event OK sẽ đóng các vấn đề đang mở do Trigger tạo ra và có ít nhất một giá trị thẻ phù hợp. Thẻ được xác định bởi cài đặt Trigger 'Thẻ cho phù hợp'. 

## 2.4 Event correlation
- Tương quan event (còn gọi là tương quan event toàn cầu) là một cách để thiết lập quy tắc đóng event tùy chỉnh (dẫn đến tạo event OK).

- Các quy tắc xác định cách các event Problem mới được ghép nối với các event Problem hiện có và cho phép đóng event mới hoặc các event đã khớp bằng cách tạo các event OK tương ứng.

- Event corelation phải được định cấu hình rất cẩn thận, vì nó có thể ảnh hưởng tiêu cực đến hiệu suất xử lý event hoặc nếu định cấu hình sai, đóng nhiều event hơn dự định (trong trường hợp xấu nhất, thậm chí tất cả các event có thể bị đóng).
- Một số mẹo cấu hình:
  - luôn giảm phạm vi tương quan bằng cách đặt một thẻ duy nhất cho event kiểm soát (event được ghép nối với các event cũ) và sử dụng điều kiện tương quan 'thẻ event mới'
  - đừng quên thêm một điều kiện dựa trên event cũ khi sử dụng thao tác 'đóng event cũ', nếu không tất cả các vấn đề hiện có có thể được đóng lại
  - tránh sử dụng các tên thẻ phổ biến được sử dụng bởi các cấu hình tương quan khác nhau

## 2.5 Task manager
- Nếu Trigger bật cài đặt 'Cho phép đóng thủ công', thì có thể đóng các `event Problem` do Trigger tạo theo cách thủ công.
- Điều này được thực hiện trong giao diện người dùng khi cập nhật Problem.
- Event không được đóng trực tiếp - thay vào đó, một tác vụ `clouses event` được tạo, sẽ được Task manager xử lý trong thời gian ngắn. 
- `Task manager` sẽ tạo ra một event OK tương ứng và event Problem sẽ được đóng lại.




# 3 Nguồn event khác
## 3.1 Service events
- Các service event chỉ được tạo nếu các hành động dịch vụ cho các event này được bật.
- Mỗi thay đổi trạng thái dịch vụ sẽ tạo ra một event mới:
  - `Problem event` - khi trạng thái dịch vụ được thay đổi từ OK thành PROBLEM
  - `OK event` - khi trạng thái dịch vụ được thay đổi từ PROBLEM thành OK

Event này chứa thông tin chi tiết về sự thay đổi trạng thái dịch vụ - khi nó xảy ra và trạng thái mới là gì.

## 3.2 Discovery events
- Zabbix định kỳ quét các dải IP được xác định trong network discovery rules (các quy tắc khám phá mạng). Tần suất check có thể được cấu hình. 
- Khi một host hoặc một dịch vụ được phát hiện, một Discovery event (hoặc một số event) sẽ được tạo ra.

Zabbix tạo ra các event sau:

|STT|Event|Khi được tạo ra|
|:---:|:---:|---|
1| `Service Up`|	Mỗi khi Zabbix phát hiện dịch vụ đang hoạt động.
2|`Service Down`|	Mỗi khi Zabbix không thể phát hiện dịch vụ.
3|`Host Up`|Nếu ít nhất một trong các dịch vụ được UP cho IP.
4|`Host Down`|Nếu tất cả các dịch vụ không phản hồi.
5|`Service Discovered`|Nếu dịch vụ hoạt động trở lại sau thời gian ngừng hoạt động hoặc được phát hiện lần đầu tiên.
6|`Service Lost`|	Nếu dịch vụ bị mất sau khi lên.
7|`Host Discovered`|Nếu máy chủ hoạt động trở lại sau thời gian ngừng hoạt động hoặc được phát hiện lần đầu tiên.
8|`Host lost`|Nếu máy chủ bị mất sau khi lên.

## 3.3 Event tự động phát hiện Agent đang hoạt động
- Event tự động đăng ký Agent đang hoạt động sẽ được tạo khi Agent hoạt động không xác định trước đó yêu cầu kiểm tra hoặc nếu metadata host đã thay đổi. 
- Server tự động thêm một host mới , sử dụng địa chỉ IP đã nhận và cổng của Agent.

## 3.3 Internall events
- Các event nội bộ xảy ra khi:
  - Một item thay đổi trạng thái từ normal - 'bình thường' thành unsupported - 'không được hỗ trợ'
  - Một item thay đổi trạng thái từ `unsupported` thành `normal`
  - Một low-level discovery rule thay đổi trạng thái từ `normal` thành `unsupported`
  - Một low-level discovery rule thay đổi trạng thái từ `unsupported` thành `normal`
  - Một Trigger thay đổi trạng thái từ `normal` thành `unsupported`
  - Một Trigger thay đổi trạng thái từ `unsupported` thành `normal`

- Các event nội bộ được hỗ trợ kể từ Zabbix 2.2.
- Mục đích : cho phép người dùng được thông báo khi bất kỳ event nội bộ nào diễn ra, chẳng hạn như một item không được hỗ trợ và ngừng thu thập dữ liệu.

# 4 Đóng thủ công các PROBLEM
## 4.1 Tổng quan
- Có những trường hợp khó xác định xem `Problem` đã được giải quyết hay chưa bằng `Trigger expression`. Khi đó, `Problem` cần được giải quyết theo cách thủ công (`manually`).

- Ex: syslog có thể báo cáo rằng một số tham số hạt nhân cần được điều chỉnh để có hiệu suất tối ưu. Trong trường hợp này, Problem được báo cáo cho quản trị viên Linux, họ sẽ khắc phục Problem và sau đó đóng Problem theo cách thủ công.

- `Problem` chỉ có thể được đóng `theo cách thủ công` đối với các `Trigger` có tùy chọn `Allow manual close` đã bật .

- Khi Problem được "đóng theo cách thủ công", Zabbix sẽ tạo một tác vụ nội bộ mới cho Zabbix server. Sau đó, quá trình task manager thực thi tác vụ này và tạo ra một `event OK`, do đó đóng `event Problem`.

- Problem được đóng theo cách thủ công vẫn có thể chuyển sang trạng thái `Problem`. Trigger expression được đánh giá lại và có thể dẫn đến Problem:
  - Khi dữ liệu mới đến cho bất kỳ item nào được bao gồm trong Trigger expression
  - Khi các hàm dựa trên thời gian được sử dụng trong biểu thức.
## 4.2 Cấu hình
Cần có hai bước để Close Problem theo cách thủ công.

###  4.2.1 Trigger configuration
- Trong cấu hình Trigger, bật tùy chọn `Allow manual close` .

### 4.2.2 Problem update window
- Nếu Problem phát sinh đối với Trigger với cờ Đóng thủ công, bạn có thể mở cửa sổ bật lên cập nhật Problem của Problem đó và đóng Problem theo cách thủ công.

- Để đóng Problem, hãy chọn tùy chọn `Close problem` trong form và click vào `Update` .

- Yêu cầu được server Zabbix xử lý . Thông thường sẽ mất một vài giây để đóng problem. Trong quá trình đó `CLOSING` được hiển thị trong `Monitoring` → `Problem` là trạng thái của Problem.

### 4.3 Xác minh
- Có thể xác minh rằng Problem đã được đóng theo cách thủ công:
  - Trong chi tiết event, thông qua `Monitoring` → `Problem` ;
  - Sử dụng macro {EVENT.UPDATE.HISTORY} trong các tin nhắn thông báo sẽ cung cấp thông tin này.


# Tài liệu tham khảo

1. https://www.zabbix.com/documentation/current/en/manual/config/events
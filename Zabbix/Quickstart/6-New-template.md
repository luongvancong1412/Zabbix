<h1> Thêm mẫu mới <h1>

<h2> Mục lục </h2>

- [1. Tổng quan](#1-tổng-quan)
- [2. Thêm mẫu](#2-thêm-mẫu)
- [3. Thêm item vào Template](#3-thêm-item-vào-template)
- [4. Link template với host](#4-link-template-với-host)
- [5. Liên kết các template được xác định trước với hosts](#5-liên-kết-các-template-được-xác-định-trước-với-hosts)
- [Tài liệu tham khảo](#tài-liệu-tham-khảo)

# 1. Tổng quan


- Khi có nhiều host ví dụ như một nghìn host. Tự động hóa (automation) là điều cần thiết.

- Lúc này cần sự trợ giúp của các mẫu (template). 
- Mẫu cho phép nhóm các item hữu ích, trigger và các thực thể khác có thể được sử dụng lại nhiều lần. Áp dụng các mẫu này cho host trong một bước duy nhất (single step).

- Khi một mẫu được link với một host, host đó sẽ kế thừa tất cả các thực thể của mẫu. Vì vậy, về cơ bản, một loạt các check được chuẩn bị trước có thể được áp dụng rất nhanh chóng.

# 2. Thêm mẫu
- Để tạo một mẫu, chọn `Configuration` → `Templates` , click vào Create template.

<img>

- Tất cả các trường bắt buộc được đánh dấu bằng dấu hoa thị `*` màu đỏ.

<h3>Các trường bắt buộc:</h3>

<h4>Template name</h4>

- Nhập tên mẫu. 
- Cho phép chữ số, dấu cách và dấu gạch dưới.

<h4>Groups</h4>

- Chọn một hoặc một số nhóm bằng cách nhấp vào nút `Select` . - Mẫu phải thuộc về một nhóm.

Cuối cùng, click vào `Add` . Mẫu mới sẽ hiển thị trong danh sách các mẫu.

<img>

- Trong hình, mẫu vừa tạo không chứa gì trong đó - không có items, triggers hoặc các thực thể khác.


# 3. Thêm item vào Template

- Để thêm một item vào mẫu, chuyển đến danh sách item cho host đó. Trong Configuration → Hosts , click vào Item của host đó.

Sau đó:

- Đánh dấu hộp kiểm của item 'CPU Load' trong danh sách
- Bấm vào Copy bên dưới danh sách
- Select mẫu để sao chép item vào

<img>

- Tất cả các trường bắt buộc được đánh dấu bằng dấu hoa thị `*` màu đỏ.

- Click vào Copy.

Nếu bây giờ bạn đi tới Configuration → Template , Mẫu mới sẽ có một item mới trong đó.

# 4. Link template với host

- Với một Template đã sẵn sàng (ready), chỉ cần thêm nó vào Host bằng cách chọn Configuration → Hosts , click vào host để mở biểu mẫu thuộc tính của nó và tìm trường Mẫu .

- Bắt đầu nhập Template mới vào trường Templates . Tên của mẫu đã tạo sẽ xuất hiện trong danh sách thả xuống. Cuộn xuống để chọn.

<img>

- Nhấp vào Update trong biểu mẫu để lưu các thay đổi. Mẫu hiện đã được thêm vào host, với tất cả các thực thể mà nó nắm giữ.

- Có thể áp dụng cho bất kỳ máy chủ nào khác. Bất kỳ thay đổi nào đối với các item, trigger và các thực thể khác ở cấp mẫu sẽ truyền đến các host mà mẫu được link.

# 5. Liên kết các template được xác định trước với hosts
- Zabbix đi kèm với một tập hợp các mẫu được xác định trước cho các hệ điều hành, thiết bị và ứng dụng khác nhau. 
- Để bắt đầu giám sát nhanh chóng, bạn có thể liên kết một trong số chúng thích hợp với một máy chủ lưu trữ.
- Lưu ý rằng các mẫu này cần được tinh chỉnh cho phù hợp với môi trường của bạn. 
- Một số kiểm tra có thể không cần thiết và khoảng thời gian bỏ phiếu có thể quá thường xuyên.


# Tài liệu tham khảo

1. https://www.zabbix.com/documentation/current/en/manual/quickstart/template
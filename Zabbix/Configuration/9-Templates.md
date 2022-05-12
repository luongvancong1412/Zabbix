<h1> Templates </h1>

<h2>Mục lục</h2>

- [1. Tổng quan](#1-tổng-quan)
- [2. Cấu hình 1 template](#2-cấu-hình-1-template)
- [3. Liên kết/Huỷ liên kết](#3-liên-kếthuỷ-liên-kết)
- [4. Nesting](#4-nesting)
- [5. Mass update](#5-mass-update)
- [Tài liệu tham khảo](#tài-liệu-tham-khảo)

# 1. Tổng quan
- Templates là một tập hợp các thực thể có thể được áp dụng nhanh cho nhiều host.

- Các thực thể có thể là:
  - items
  - triggers
  - graphs
  - dashboards
  - low-level discovery rules
  - web scenarios

- Trên thực tế có nhiều host cấu hình giống nhau, với các mẫu, ta có thể sao chép chúng vào một Templates và sau đó áp dụng Templates cho nhiều host nếu cần.

- Khi một template được liên kết với host, tất cả các thực thể (items, triggers, graphs,...) của template sẽ được thêm vào host. Các template được chỉ định trực tiếp cho từng host riêng lẻ (chứ không phải cho một nhóm host).

- Các template thường được sử dụng để nhóm các thực thể cho các dịch vụ hoặc ứng dụng cụ thể (như Apache, MySQL, PostgreSQL, Postfix...) và sau đó áp dụng cho các host chạy các dịch vụ đó.

- Ngoài ra, khi cần thay đổi 1 cái gì đó trong các host. Cấu hình template từ một lần sẽ truyền thay đổi đến tất cả các host được liên kết.

Do đó, Sử dụng các template là một cách để giảm khối lượng công việc của một người và hợp lý hóa cấu hình Zabbix.

# 2. Cấu hình 1 template

# 3. Liên kết/Huỷ liên kết

# 4. Nesting

# 5. Mass update

# Tài liệu tham khảo

1. https://www.zabbix.com/documentation/current/en/manual/config/templates
<h1> Nhận cảnh báo qua Telegram/Gmail<h1>

<h2> Mục lục </h2>

- [I. Telegram webhook](#i-telegram-webhook)
  - [1. Thiết lập Telegram](#1-thiết-lập-telegram)
    - [1.1 Tạo Telegram BOT mới](#11-tạo-telegram-bot-mới)
    - [1.2 Gửi thông báo tới cá nhân](#12-gửi-thông-báo-tới-cá-nhân)
    - [1.3 Gửi thông báo tới nhóm](#13-gửi-thông-báo-tới-nhóm)
  - [2. Thiết lập Zabbix](#2-thiết-lập-zabbix)
  - [3. Cấu hình User](#3-cấu-hình-user)
- [II. Gmail](#ii-gmail)
  - [1. Cấu hình Media Type Email: Gmail](#1-cấu-hình-media-type-email-gmail)
  - [2. Test cảnh báo qua gmail](#2-test-cảnh-báo-qua-gmail)
  - [3. Cấu hình địa chỉ Gmail cho User](#3-cấu-hình-địa-chỉ-gmail-cho-user)
  - [4. Kết quả](#4-kết-quả)
- [Tài liệu tham khảo](#tài-liệu-tham-khảo)

Hướng dẫn này mô tả cách gửi thông báo từ Zabbix 6.0 tới Telegram messenger bằng cách sử dụng Telegram Bot API và tính năng webhook của Zabbix.

# I. Telegram webhook

Các tính năng:
- Personal and group notifications
- Markdown/HTML support
## 1. Thiết lập Telegram

### 1.1 Tạo Telegram BOT mới
- Gửi `/newbot` tới `@BotFather` và làm theo hướng dẫn

![Imgur](https://i.imgur.com/IHHIDy6.png)

### 1.2 Gửi thông báo tới cá nhân

- Lấy ID chat của người dùng mà BOT sẽ gửi tin nhắn:

![Imgur](https://i.imgur.com/DLoyznc.png)

### 1.3 Gửi thông báo tới nhóm

- Nếu bạn muốn gửi thông báo nhóm, bạn cần lấy ID nhóm của nhóm mà bot sẽ gửi tin nhắn
  - Thêm "@myidbot" và "@your_bot_name_here" vào nhóm của bạn. 
  - Gửi tin nhắn "/ getgroupid @ myidbot" trong nhóm. 
  - Trong cuộc trò chuyện nhóm, hãy gửi "/ start @ your_bot_name_here".

![Imgur](https://i.imgur.com/6JNdyFr.png)

![Imgur](https://i.imgur.com/3kXCqk4.png)

## 2. Thiết lập Zabbix

- Chọn: `Administration` > `Media types` > `Telegram`

![Imgur](https://i.imgur.com/7iHsaZB.png)

- Copy và Paste Telegram Bot Token vào trường `Token`:

![Imgur](https://i.imgur.com/EeWJnw0.png)

- Trong đó: Trường ParseMode có 3 option:
  - Markdown
  - HTML
  - MarkdownV2

<h3> Kiểm tra Media type</h3>

- Kiểm tra bằng cách chọn Test trong hàng Telegram
- Điền Nội dung tin và ID nhóm hoặc ID cá nhân nhận cảnh báo. Click vào `Test` để gửi.
![Imgur](https://i.imgur.com/Xjh7KBC.png)

- Kết quả:

![Imgur](https://i.imgur.com/9wV7mHn.png)

## 3. Cấu hình User

- Bước 1: Chọn `Administration` > `User`

![Imgur](https://i.imgur.com/IMTvqys.png)

- Bước 2: Chọn `User` muốn thêm. Ex: `Admin`

![Imgur](https://i.imgur.com/GDfqDW5.png)

- Bước 3: Chọn `Media` > `Add`

![Imgur](https://i.imgur.com/D4fjxuP.png)

- Bước 4: Chọn `Type` > `Telegram`. `Send to` nhập ID group hoặc ID cá nhân. Chọn thời gian gửi:`1-7,06:00-18:00`

![Imgur](https://i.imgur.com/YDwowYl.png)

- Bước 5: Chọn Update để cập nhật thông tin user

![Imgur](https://i.imgur.com/Alh7HOS.png)

- Kết quả:

![Imgur](https://i.imgur.com/MTEPTIQ.png)

# II. Gmail
## 1. Cấu hình Media Type Email: Gmail
- Chọn `Administration` > `Media types` > `Email`.

![Imgur](https://i.imgur.com/CrViiPg.png)

- Nhập các thông tin:
  - SMTP server: `smtp.gmail.com`
  - SMTP server port: `587`
  - SMTP helo: `smtp.gmail.com`
  - SMTP email: `luongvancong070129@gmail.com`
  - Connection security:` STARTTSL`
  - Authntication: `Username and password`
  - Nhập username, passwd
  - Chọn `Update`

![Imgur](https://i.imgur.com/jssBET8.png)

- Đăng nhập qua trình duyệt bằng tài khoản Gmail đã cấu hình và truy cập: https://myaccount.google.com/lesssecureapps
- Bật chức năng: `Cho phép ứng dụng kém an toàn`

![Imgur](https://i.imgur.com/b39RMGF.png)

## 2. Test cảnh báo qua gmail
- Chọn: Administration → Media types
- Click vào `Test` trên dòng Email

![Imgur](https://i.imgur.com/biqqkeS.png)

- Nhập gmail nhận cảnh báo qua `Send to`:

- Click vào `Test` để kiểm tra

![Imgur](https://i.imgur.com/b6le6HZ.png)

- Kết quả:

![Imgur](https://i.imgur.com/D0BPQGV.png)

## 3. Cấu hình địa chỉ Gmail cho User
- Chọn `Administration` > `Users` > Chọn user `Admin` 
- Click vào Tab `Media` , chọn `Add`
- Chọn Type: `Email`
- Send to: `luongvancong70129@gmail.com`
- Thời gian: 1-7,06:00-22:00
- Chọn `Add` để thêm

![Imgur](https://i.imgur.com/D0BPQGV.png)

## 4. Kết quả

![Imgur](https://i.imgur.com/E0XDKpw.png)
# Tài liệu tham khảo

1. https://git.zabbix.com/projects/ZBX/repos/zabbix/browse/templates/media/telegram?at=refs%2Fheads%2Frelease%2F6.0
2. https://kb.kdata.vn/zabbix-cau-hinh-telegram-715/
3. https://bestmonitoringtools.com/zabbix-alerts-setup-zabbix-email-notifications-escalations/
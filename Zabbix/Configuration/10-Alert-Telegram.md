<h1> Nhận cảnh báo qua Telegram <h1>

<h2> Mục lục </h2>

Hướng dẫn này mô tả cách gửi thông báo từ Zabbix 6.0 tới Telegram messenger bằng cách sử dụng Telegram Bot API và tính năng webhook của Zabbix.

# 1. Telegram webhook

Các tính năng:
- Personal and group notifications
- Markdown/HTML support
# 1. Thiết lập Telegram

## 1.1 Tạo Telegram BOT mới
- Gửi `/newbot` tới `@BotFather` và làm theo hướng dẫn

![Imgur](https://i.imgur.com/IHHIDy6.png)

## 1.2 Gửi thông báo tới cá nhân

- Lấy ID chat của người dùng mà BOT sẽ gửi tin nhắn:

![Imgur](https://i.imgur.com/DLoyznc.png)

## 1.3 Gửi thông báo tới nhóm

- Nếu bạn muốn gửi thông báo nhóm, bạn cần lấy ID nhóm của nhóm mà bot sẽ gửi tin nhắn
  - Thêm "@myidbot" và "@your_bot_name_here" vào nhóm của bạn. 
  - Gửi tin nhắn "/ getgroupid @ myidbot" trong nhóm. 
  - Trong cuộc trò chuyện nhóm, hãy gửi "/ start @ your_bot_name_here".

![Imgur](https://i.imgur.com/6JNdyFr.png)

![Imgur](https://i.imgur.com/3kXCqk4.png)

# 2. Thiết lập Zabbix

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

# 3. Thêm user nhận cảnh báo

- Updating ...

# Tài liệu tham khảo

1. https://git.zabbix.com/projects/ZBX/repos/zabbix/browse/templates/media/telegram?at=refs%2Fheads%2Frelease%2F6.0
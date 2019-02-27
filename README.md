# mt4-telegram
Phần 1. Tạo Telegram bot và lấy ChatID
1.1 Để tạo con bot thực hiện việc gửi nhận tin nhắn trên Telegram, thực hiện chat với Bot Farther của Telegram là @BotFather
 - /newbot -> Đặt tên cho con bot (Tùy ý, VD: Demo MT4 Bot). Sau đó tạo nick name (không dấu cách, viết liền, và kết thúc bằng từ bot, VD: demo_telegram_mt4_bot).
Sau khi thực hiện xong thì Bot Father sẽ tạo một con bot có link http://t.me/demo_telegram_mt4_bot và HTTP Token, bạn copy cái HTTP Token lại để cấu hình vào Telegram Forward Server (TFS)
2.1 Lấy chat id, đây là ID của account telegram của bạn, hoặc ID của group nếu bạn muốn gửi tin nhắn vào Group. Để lấy chat id của Account thì bạn chat với bot: @get_id_bot. Nếu muốn lấy ID của Group thì bạn thêm con bot @RawDataBot vào Group, nó sẽ tự động lấy ID của group.
Lưu ý: Để bot của telegram có thể gửi tin nhắn vào Group thì phải cấu hình Group Privacy Off trong mục Bot Settings ở @BotFather

Phần 2. Cài đặt Telegram Bot EA trên MT4
2.1 Mở thư mục chứa Expert Advisors (EA) của MT4 (File -> Open Data Folder) -> MQL4 ->Experts. Copy file TelegramBot.ex4 vào thư mục đó.
2.2 Cho phép EA sử dụng DLL, EA cần gửi dữ liệu tin nhắn khi có lệnh đóng/mở sang TFS vì vậy nó sử dụng thư viện DLL có sẵn, mặc định MT4 tắt chức năng này, do vậy bạn cần phải Allow DLL Imports (Mục Tools -> Options -> Tab Expert Advisors -> chọn Allow DLL Imports
2.3 Mở 1 chart của một cặp bất kỳ để thêm TelegramBot EA vào, chart này phải luôn được bật và bật chế độ AutoTrading (Đây không phải bot tự trade, nhưng nó là EA nên phải bật chức năng đó để TelegramBot EA có thể hoạt động)
2.4: Cấu hình các thông số của TelegramBot EA:
- ServerIP: Địa chỉ của Telegram Forward Server (TFS), nếu chạy máy tính cùng với MT4 thì mặc định là: localhost (127.0.0.1 hoặc địa chỉ IP LAN của máy đó)
- ServerPort: Cổng truy cập của TFS (Mặc định là 80, vì TFS là một Web Server thông thường, nếu bạn muốn dùng port khác thì cấu hình trong file config.json của TFS và ở đây)
- TelegramChatID: là chat id lấy được từ phần 1, có thể là chat id của account, hay của Group, tùy thuộc vào việc bạn muốn tin nhắn đi đến đâu (Bot hay vào Group)
- RefreshSec: Thời gian tính bằng giây giữa các lần quét lệnh, mặc định là quét liên tục 1s/1 lần. Nếu tần suất đóng/mở lệnh của bạn không cao, có thể tăng giá trị này để đỡ tốn tài nguyên
Phần 3. Cài đặt Telegram Forward Server và kích hoạt quyền sử dụng.
Telegram Forward Server (TFS) là thành phần không thể thiếu để sử dụng TelegramBot EA, nó là Web Server (máy chủ web) trung gian gửi lệnh từ EA trên MT4 đến máy chủ của Telegram để gửi tin nhắn. Do đó TFS phải được bật liên tục, đơn giản bằng cách chạy file server-telegram.exe (Trên Windows, nếu bạn chạy các nền tảng khác thì liên hệ mình lấy bản chạy cho nền tảng đó).
- TFS có thể chạy trực tiếp trên cùng máy tính với MT4 hoặc cài đặt trên VPS nếu muốn.
- TFS sẽ kiểm soát bản quyền sử dụng của người dùng, thông qua email và số tài khoản MT4 của sàn mà bạn đang sử dụng. Người dùng khi mua/thuê sản phẩm này phải cung cấp email và tài khoản nếu cần để kích hoạt trên hệ thống quản lý. Sau khi được kích hoạt thì người dùng cấu hình vào mục tương ứng trong file config.json.
- Trước khi chạy TFS, người dùng phải đảm bảo các thông số trong file config.json (trong cùng thư mục với server-telegram.exe) là đã chuẩn. Các thông số như sau:
 + http -> port: mặc định 80, là port của TFS sẽ sử dụng, đảm bảo là chưa ứng dụng nào sử dụng port này, nếu trùng có thể thay thế bằng port khác, và cấu hình trong cả TelegramBot EA ở phần 2 tương ứng.
 + token: Đây là HTTP token của bot được tạo ra bởi BotFather của hệ thống Telegram, ở phần 1 đã nói rõ.
 + license: Loại license (bản quyền sử dụng) mà người dùng được cấp, chi tiết liên hệ bên cung cấp để được rõ license bạn được sử dụng.
 + email: email dùng để kích hoạt license
 + account: account dùng để kích hoạt license, nếu license của bạn bị giới hạn theo số tài khoản (Account number) của sàn thì bạn phải nhập đúng tài khoản đã gửi cho chúng tôi kích hoạt trước đó, nếu sai sẽ không sử dụng được.
Chi tiết và hỗ trợ vui lòng liên hệ Telegram @siwtom hoặc người bán.

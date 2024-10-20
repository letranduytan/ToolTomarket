# Tool Auto Tomarket NodeJS by Duytan

**Tool phát triển và chia sẻ miễn phí bởi Duytan**

<a href="https://www.facebook.com/duytan.hh">Facebook</a>
<a href="https://t.me/duytan2003">Telegram</a>


## 🛠️ Hướng dẫn cài đặt

> Yêu cầu đã cài đặt NodeJS

- Bước 1: Tải về phiên bản mới nhất của tool 
- Bước 2: Giải nén tool
- Bước 3: Tại thư mục tool vừa giải nén, chạy lệnh `npm install` để cài đặt các thư viện bổ trợ

## 💾 Cách thêm dữ liệu tài khoản

> Tool hỗ trợ cả `user` và `query_id` (khuyến khích dùng user)

> Tất cả dữ liệu mà bạn cần nhập đều nằm ở các file trong thư mục 📁 `src / data`

- [users.txt](src/data/users.txt) : chứa danh sách `user` hoặc `query_id` của các tài khoản, mỗi dòng ứng với một tài khoản
- [proxy.txt](src/data/proxy.txt) : chứa danh sách proxy, proxy ở mỗi dòng sẽ ứng với tài khoản ở dòng đó trong file users.txt phía trên, để trống nếu không dùng proxy
- [wallet.txt](src/data/wallet.txt) : chứa danh sách địa chỉ ví TON muốn liên kết, địa chỉ ví mỗi dòng sẽ ứng với tài khoản ở dòng đó trong file users.txt phía trên, để trống hoặc gõ `skip` nếu không muốn chạy liên kết ví.
- [token.json](src/data/token.json) : chứa danh sách token được tạo ra từ `user` hoặc `query_id`. Có thể copy token từ các tool khác qua file này (miễn cùng format) để chạy.

> Định dạng proxy: http://user:pass@ip:port

> Lưu ý: `user` và `query_id` chỉ có thời gian sống (có thể get token) trong tầm 1-2 ngày, `token` có thời gian sống 30 ngày. Vậy nên nếu nhận được thông báo đăng nhập thất bại, hãy lấy mới lại `user` hoặc `query_id`

## >\_ Các lệnh và chức năng tương ứng

| Lệnh             | Chức năng                                                                            |
| ---------------- | ------------------------------------------------------------------------------------ |
| `npm run start`  | Dùng để chạy claim, làm nhiệm vụ, chơi game,.... tóm lại game có gì là nó làm cái đó |
| `npm run wallet` | Dùng để liên kết ví                                                                  |

## 🕹️ Các tính năng có trong tool

- tự động daily check-in
- tự động làm nhiệm vụ
- tự động làm daily combo
- tự động claim
- tự động chơi game
- tự động nhận rank và nâng cấp rank
- tự động quay số
- tự đông làm Puzzle
- nhận diện proxy tự động, tự động kết nối lại proxy khi bị lỗi. ae ai chạy proxy thì thêm vào file proxy.txt ở dòng ứng với dòng chứa acc muốn chạy proxy đó, acc nào không muốn chạy proxy thì để trống hoặc gõ skip vào
- đa luồng chạy bao nhiêu acc cũng được, không bị block lẫn nhau, lặp lại khi tới thời gian chơi game
- hiển thị đếm ngược tới lần chạy tiếp theo, có thể tìm biến `IS_SHOW_COUNTDOWN = true` đổi thành `false` để tắt cho đỡ lag

> [!WARNING]
>
> - Có thể đặt số lần quay số (spin) tối đa bằng sao (star), tối đa 3, tối thiểu 0, mặc định là 0 (không dùng). Tìm biến `MAX_SPIN_STAR = 0` để thay đổi
> - có thể đặt giới hạn số lượt quay số (spin) miễn phí, tối thiểu 0 - không quay số, mặc định là 1. Tìm biến `MIN_SPIN_FREE = 1` để thay đổi
> - Chỉ tự chạy nâng cấp rank khi đủ số sao để nâng cấp
> - Chỉ có thể liên kết ví với các tài khoản chưa liên kết ví
> - Địa chỉ ví dùng để liên kết phải là địa chỉ ví mạng TON, được tạo từ Bitget Wellet

## ♾ Cài đặt đa luồng

- Mặc định tool sẽ chạy đa luồng ứng với số tài khoản bạn nhập vào, không cần cài đặt thêm gì cả.
- Mặc định ở vòng lặp đầu tiên mỗi tài khoản (luồng) sẽ chạy cách nhau 10s để tránh spam request, có thể tìm biến `DELAY_ACC = 10` trong file [index.js](src/run/index.js) để điều chỉnh cho phù hợp

## ❌ Chế độ thử lại khi lỗi

- Đỗi với lỗi kết nối proxy, hệ thống sẽ cố thử lại sau mỗi 30s, bạn có thể cài đặt giới hạn số lần thử lại bằng cách tìm biến `MAX_RETRY_PROXY = 20` trong file [index.js](src/run/index.js) để điều chỉnh cho phù hợp (mặc định là 20). Khi quá số lần thử kết nối lại hệ thống sẽ dừng auto tài khoản đó và nghi nhận lỗi vào file [log.error.txt](src/data/log.error.txt)
- Đỗi với lỗi đăng nhập thất bại, hệ thống sẽ cố thử lại sau mỗi 60s, bạn có thể cài đặt giới hạn số lần thử lại bằng cách tìm biến `MAX_RETRY_LOGIN = 20` trong file [index.js](src/run/index.js) để điều chỉnh cho phù hợp (mặc định là 20). Khi quá số lần thử đăng nhập lại hệ thống sẽ dừng auto tài khoản đó và nghi nhận lỗi vào file [log.error.txt](src/data/log.error.txt)


  


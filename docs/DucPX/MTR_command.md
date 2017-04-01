# Chuẩn đoán mạng với MTR (My Trace Router)

## Giới thiệu
- MTR là một công cụ chuẩn đoán network mạnh mẽ, cho phép administrators chuẩn đoán và cô lập lỗi mạng và cung cấp các báo cáo hữu ích về tình trạng mạng.
- MTR là một công cụ tiến hóa hơn `traceroute` bằng cách cung cấp data mẫu lớn hơn, tham số vào là traceroute và đầu ra là ping.
- Các công cụ chuẩn đoán mạng bao gồm như ping, traceroute và mtr đều sử dụng gói tin ICMP để kiểm tra kết nối và traffic giữa 2 points trên internet. Khi ping tới 1 host, 1 loạt gói tin ICMP được gửi tới host, host đáp lại bằng cách gửi các gói tin trở lại. Trên máy client mà nhận được phản hồi, sẽ có khả năng tính toán ra thời gian đi và về của gói tin giữa hai points trên internet.
- Thay vì đưa ra 1 bản phác thảo đơn giản về tuyến đường như lệnh traceroute thì mtr sẽ thu thập thông tin bổ sung về trạng thái, kết nối và khả năng phản hồi của các máy chủ trung gian.
- MTR cần phải được cài đặt (MTR không có sẵn trong các bản distro của linux)

`sudo apt-get install -y mtr`

## Một số tùy chọn của MTR
- `-r hoặc --report`: tùy chọn này đặt mtr vào chế độ report. Khi trong chế độ này, mtr sẽ chạy với số chu kỳ được chỉ rõ trong tùy chọn **-c**, sau đó in ra thống kê và thoát. Chế độ này rất hữu ích cho việc sinh ra thống kê cho chất lượng mạng. ![Imgur](http://i.imgur.com/JjsMIoE.png)
- `-w hoặc --report-wide`: tùy chọn này đặt mtr vào chế độ report wide, mtr sẽ không cắt hostname vào trong báo cáo. ![Imgur](http://i.imgur.com/BxybjO4.png)
- `-c COUNT hoặc --report-cycles COUNT`: tùy chọn này thiết lập số lượng ping sẽ gửi để xác định cả hai máy trên cùng một mạng và độ tin của chúng. Mỗi chu kỳ là 2 giây. ![Imgur](http://i.imgur.com/wwSfhrp.png)
- `-n hoặc --no-dns`: Tùy chọn này để mtr chỉ hiện thị địa chỉ IP. ![Imgur](http://i.imgur.com/h1oAsA0.png)
- `-b hoặc --show-ips`: sẽ có cả ip và hostname trong báo cáo. Sử dụng thêm tùy chọn -w để hiện thị đầy đủ ip và hostname, nếu không địa chỉ ip sẽ bị chặt mất một phần nếu tên hostname quá dài. ![Imgur](http://i.imgur.com/LEt6Lqv.png)
- `-o`: sắp đặt thứ tự các trường
	- tất cả các trường: 
	- ![Imgur](http://i.imgur.com/HB045wI.png)
	- ví dụ `-o "LSD NBAW"`
	- ![Imgur](http://i.imgur.com/hJcdK6p.png)

- `-a IP.ADD.RE.SS`: sử dụng tùy chọn này để chỉ rõ interface nào mà các gói tin sẽ đi ra. Địa chỉ IP là có sẵn trên máy tính. Tùy chọn này chỉ để xác là là interface chứ không phải là gán địa chỉ ip cho interface. ![Imgur](http://i.imgur.com/0oACRpt.png)

---
#### Trên đây là một số tùy chọn của lệnh mtr. Để xem hết tất cả các tùy này của mtr, dùng lệnh `man mtr` sẽ liệt kê ra tất cả tùy chọn và miêu tả cách sử dụng.


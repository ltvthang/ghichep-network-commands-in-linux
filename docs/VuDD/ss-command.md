# Báo cáo lệnh ss (socket statistics)



## Mục lục
[1.Giới thiệu](#1)

[2.Một số tuỳ chọn của lệnh ss](#2)

<a name='1'></a>
## 1.Giới thiệu

-Lệnh ss cũng tương tự như lệnh netstat nhưng hiển thị nhiều thông tin hơn so với netstat và nhanh hơn netstat.

-Lệnh netstat đọc nhiều tập /proc để thu thập thông tin, tuy nhiên phương pháp tiếp cận này giảm sút khi có nhiều kết nối
để hiển thị, điều này làm cho nó chậm hơn so với lệnh ss

-Lệnh ss nhận thông tin trực tiếp từ không gian hạt nhân. Các tuỳ chọn được sử dụng với lệnh ss rất giống với netstat làm
cho nó dễ dàng thay thế netstat.

-Lệnh ss có thể cung cấp thông tin về:
    - Tất cả TCP socket
    - Tất cả UDP socket
    - Tất cả thiếp lập ssh/ftp/http/https.
    - Tất cả các tiến trình local kết nối tới 1 server X
    - Cho phép lọc trạng thái kết nối như connected, synchronized, theo các địa chỉ port

<a name='2'></a>
## 2.Một số tuỳ chọn của lệnh ss

-Liệt kê tất cả các kết nối: Đây là câu lệnh đơn giản nhất để liệt kê tất cả các kết nối trên máy
   ```
   ss | less
   ```
   <img src="http://imgur.com/b2Qnf27" >


-Lọc ra các kết nối tcp, udp hoặc unix: Để xem các kết nối tcp hoặc udp hoặc unix sử dụng tùy chọn t, u hoặc x.
   ```
   ss -t
   ss -u
   ss -x
   ```
   <img src="http://imgur.com/fGUfVo0" >

   <img src="http://imgur.com/Th1dTWA" >

   -Theo mặc định, tùy chọn "t" sẽ chỉ báo cáo những kết nối "đã được thiết lập" hoặc CONNECTED ", nó không báo cáo các ổ cắm tcp" LISTENING "
  Sử dụng tùy chọn '-a' cùng với t, để báo cáo Tất cả chúng cùng một lúc.
   ```
   ss -at
   ss -au
   ss -ax
   ```
   <img src="http://imgur.com/2wgcPHs" >

-Chỉ hiển thị những socket đang lắng nghe
   ```
   ss -ltn
   ss -lun
   ```
   <img src="http://imgur.com/aWoLa4y" >

-Hiển thị tên tiến trình và PID: Để in tên quá trình/pid sở hữu kết nối sử dụng tùy chọn -p
   ```
   ss -ltp
   ss -lup
   ```
   <img src="http://imgur.com/5OaiVZ0" >

-In thống kê tóm tắt: sử dụng tuỳ chọn -s để in ra bản thống kê tóm tắt
   ```
   ss -s
   ```
   <img src="http://imgur.com/t6ttZtD" >

-Lọc các kết thôi theo trạng thái tcp: Lệnh ss hỗ trợ các bộ lọc có thể được sử dụng để chỉ hiển thị các kết nối cụ thể. Các biểu thức lọc nên
được suffixed sau khi tất cả các tùy chọn. Lệnh ss chấp nhận bộ lọc ở định dạng sau.
   ```
   ss [ OPTIONS ] [ STATE-FILTER ] [ ADDRESS-FILTER ]
   ```
   Ví dụ:
   ```
   ss -u4 state established
   ss -u4 state closed
   ```
   <img src="http://imgur.com/X6W5QNu" >

   Ngoài ra bạn có thể xem quá trình của lệnh như sau:
   ```
   watch -n 1 "ss -u4 state established"
   ```
   <img src="http://imgur.com/uZTWjHD" >

-Lọc kết nối theo địa chỉ và số cổng: Ngoài các trạng thái socket tcp, lệnh ss cũng hỗ trợ lọc theo địa chỉ và số cổng của socket
   ```
   ss -nu dst :443 or dst :80
   ss -nt dst 192.168.20.10
   ss -nt dport :=80
   .....
   ```


## Tham khảo: http://www.binarytides.com/linux-ss-command/

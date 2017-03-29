# Báo cáo về lệnh Fping

## Mục lục

[1.Giới thiệu](#1)

[2.Mốt số tuỳ chọn của Fping](#2)

<a name='1'></a>
## 1.Giới thiệu

-Fping là 1 chương trình giống như ping sử dụng yêu cầu ECHO_REQUEST của ICMP để xác định xem 1 máy chủ đích đang đáp ứng hay không
(alive)

-Fping khác với ping trong đó bạn có thể chỉ định bất kì số mục tiêu nào trên dòng lệnh hoặc chỉ định 1 tệp chứa danh sách các mục tiêu để ping

-Thay vì gửi đến 1 mục tiêu cho đến khi nó hết thời gian hoặc nó trả lời, fping sẽ gửi gói ping mà chuyển sang mục tiêu kế tiếp theo kiểu vòng robin

-Trong chế độ mặc định, nếu 1 mục tiêu trả lời, nó sẽ được ghi chú và xoá khỏi danh sách các muc tiêu để kiểm tra

-Nếu 1 mục tiêu không đáp ứng trong 1 giới hạn nhất định hoặc giới hạn thử lại, nó sẽ được chỉ định là không thể truy cập được.

-Fping cũng hỗ trợ gửi 1 số lượng ping cụ thể đến 1 mục tiêu cụ thể hoặc lặp lại vô thời hạn(giống như ping).

-Không giống như ping, fping có nghĩa là được sử dụng trong các kịch bản vì vậy đầu ra của nó được thiết kể dễ dàng phân tích cú pháp.

<a name='2'></a>
## 2.Một số tuỳ chọn của fping

\-Tuỳ chọn -a(--alive): Hiển thị hệ thống đang sống, hoạt động
   ```
   fping -a google.com.vn
   fping -a 8.8.8.8
   ```
   ![fping](http://imgur.com/pbwX7xC)

\-Tuỳ chọn -A(--addr): Hiển thị mục tiêu the đia chỉ chứ không phải tên DNS. Kết hợp vs -d đầu ra sẽ là cả IP và tên máy chủ.
   ```
   fping -A -d google.com.vn
   ```
   ![fping -A](http://imgur.com/C8MGiCI)

\-Tuỳ chọn -c: Hiển thị số yêu cầu echo_request tới mỗi đối tượng
   ```
   fping -c 5 google.com.vn
   fping -c 5 google.com.vn -c 8 8.8.8.8
   ```
   ![fping -c](http://imgur.com/5jk2E9J)

\-Tuỳ chọn -D: Hiển thị thời gian trước các gói tin phải hồi lại
   ```
   fping -D -c 5 google.com.vn
   ```
   ![fping -D](http://imgur.com/dYcufew)

\-Tuỳ chọn -e: Hiển thị thời gian trôi qua(round-trip) của các gói dữ liệu
   ```
   fping -e google.com.vn
   ```
   ![fping -e](http://imgur.com/QxZiN3U)

\-Tuỳ chọn -n: Nếu các mục tiêu được chỉ định là địa chỉ IP, hãy tra cứu DNS ngược lại để chúng
   ```
   fping -n google.com.vn
   fping -n 8.8.8.8
   ```
   ![fping -n](http://imgur.com/xiJZVup)

\-Tuỳ chọn -I: Sử dụng card mạng được chỉ định
   ```
   fping -I enp0s9 google.com.vn
   fping -I enp0s8 google.com.vn
   fping -I enp0s3 google.com.vn
   ```
   ![fping -I](http://imgur.com/6tUz2gs)

\-Tuỳ chọn -s: In các số liệu thống kê tích lũy khi xuất cảnh.
   ```
   fping -s google.com.vn
   fping -s -g google.com.vn
   ```
   ![fping -s](http://imgur.com/yY0zN5T)

   ![fping -s -g](http://imgur.com/IXZiAk6)


## Tham khảo:

https://fping.org/fping.1.html

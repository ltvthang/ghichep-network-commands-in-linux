# ping and fping command

## ***Mục lục***

[1. Lệnh ping](#1)

- [1.1. Giới thiệu câu lệnh ping](#1.1)

- [1.2. Một số tùy chọn sử dụng trong câu lệnh ping](#1.2)

- [1.3. Một số ví dụ](#1.3)

[2. Lệnh fping](#2)

- [2.1. Giới thiệu](#2.1)

- [2.2. Một số tùy chọn](#2.2)

- [2.3. Một số ví dụ](#2.3)

[3. Tham khảo](#3)

---

<a name = "1"></a>
# 1. Lệnh ping

<a name = "1.1"></a>
## 1.1. Giới thiệu câu lệnh ping

- Câu lệnh **ping** được sử dụng để kiểm tra kết nối và độ trễ giữa 2 kết nối mạng. những kết nối này có thể trong mạng nội bộ hoặc trên mạng rộng như Internet. 

- Lệnh **ping** sẽ gửi các gói tin chứa thông tin để xác định một địa chỉ IP và sau đó đo thời gian cần thiết để nhận được bản tin đáp trả lại từ một máy tính hoặc thiết bị sở hữu IP đó.

- Lệnh ping làm việc trên **giao thức ICMP (Internet Control Message Protocol)** dùng để kiểm tra tình trạng kết nối mạng giữa 2 host. Lệnh ping được dùng trên tất cả các hệ điều hành như Unix, Linux, Window,… 

- Khi lệnh Ping được thực thi HOST A sẽ gởi gói tin ICMP echo request cho HOST B, khi nhận được HOST B nhận được gói tin ICMP echo request nó sẽ gởi lại gói tin ICMP echo reply (với điều kiện HOST B không bị Firewall chặn các gói tin ICMP), lúc HOST A nhận được gói tin ICMP echo reply của HOST B ta mới xác nhận rằng HOST A và HOST B đã kết nối được với nhau. Bằng cách sử dụng lệnh ping đến các Node mạng ta có thể kiểm tra được tình trạng kết nối của hệ thống mạng.

<img src = "http://imgur.com/tWIZP1s.jpg">

Tham khảo thêm về gói tin ICMP [tại đây.](https://letonphat.wordpress.com/2010/11/27/icmp-l-thuy%E1%BA%BFt-v-%E1%BB%A9ng-d%E1%BB%A5ng/)

<a name = "1.2"></a>
## 1.2. Một số tùy chọn sử dụng trong câu lệnh ping

- Cấu trúc câu lệnh:

```  
     ping  [-aAbBdDfhLnOqrRUvV]  [-c count] [-F flowlabel] [-i interval] [-I
       interface]  [-l   preload]   [-m   mark]   [-M   pmtudisc_option]   [-N
       nodeinfo_option]  [-w  deadline] [-W timeout] [-p pattern] [-Q tos] [-s
       packetsize] [-S sndbuf]  [-t  ttl]  [-T  timestamp  option]  [hop  ...]
       destination
```
 
Một số tùy chọn: 

\- **-c** *count*: Dừng lại sau khi gửi (hoặc nhận) đủ count gói tin ECHO_RESPONSE

\- **-f**: ***Flood ping*** -  Dùng dể flood các gói tin ICMP một cách nhanh nhất có thể hoặc gửi 100 lần trong mỗi giây. Được sử dụng để tấn công nhằm làm giảm băng thông trong mạng. Tùy chọn này chỉ được sử dụng với người dùng **super-user**.

\- **-i** *wait* : Chờ trong khoảng thời gian ***wait*** giữa việc gửi các gói tin. Mặc định, ping sẽ chờ 1s cho mỗi lần gửi các gói tin. 

\- **-n**: Đổi đầu ra chỉ hiển thị địa chỉ IP, không hiển thị tên miền.

\- **-q** : Quiet output - Không có gì hiển thị ra trừ các thông tin tóm tắt lúc bắt đầu gửi gói tin và lúc kết thúc ping

\- **-s** *packetsize*   : Xác định kích thước dữ liệu được gửi đi là ***packetsize***. Giá trị mặc định là 56 byte,  được đóng gói thêm 8 byte ICMP header thành 64 byte. 

\- **-I** *interface*: Chỉ định interface được dùng để gửi bản tin icmp.

\- **-l** *preload* :   Nếu ***preload*** được xác định, ping sẽ gửi gói tin icmp request đi nhiều mà không cần chờ cho reply trở về. Chỉ người dùng **super-user** mới dùng được tùy chọn này với preload nhiều hơn 3.

\- **-t** *ttl* : Set  thời gian ***Time to Live*** cho gói tin gửi đi.
         
\- **-w** *deadline*  : Xác định thời gian thực hiện lệnh ping cho đến khi dừng lại *(tính bằng giây)*

\- **-r** : Bỏ qua các bảng định tuyến thông thường và gửi trực tiếp tới host trên interface gán vào. Nếu host đó không nằm trực tiếp trên mạng thuộc về interface gửi bản tin icmp, sẽ có lỗi trả về. Tùy chọn này dùng để ping tới các host trong mạng nội bộ thông qua một interface không có định tuyến.

Tham khảo thêm các tùy chọn khác tại [manpage ping](http://manpages.ubuntu.com/manpages/xenial/man8/ping.8.html)

<a name = "1.3"></a>
## 1.3. Một số ví dụ

Dùng phím CTRL + C để dừng lại ping bất cứ lúc nào. 

### 1) Ping tới địa chỉ broadcast:

`ping 10.10.10.255 –b`

<img src = "http://imgur.com/oLYsF3L.jpg">

Kết quả bắt trên wireshark máy có interface 10.10.10.10:

<img src = "http://imgur.com/0BSLhHD.jpg">

### 2) Gửi 5 gói tin ICMP request, mỗi gói gửi cách nhau 5s:

`ping –i 5 –c 5 8.8.8.8`

<img src = "http://imgur.com/tft627m.jpg">

Bắt trên wireshark theo dõi thời gian gửi gói tin: 

<img src = "http://imgur.com/H7TGWxB.jpg">

### 3) Gửi ping với tùy chọn –n cho đầu ra không ánh xạ ra tên miền:

<img src = "http://imgur.com/4xWQ66X.jpg">

### 4) Gửi bản tin ICMP với kích thước gói tin tùy ý với tùy chọn –s:

<img src = "http://imgur.com/U4N01Ws.jpg">

### 5) Thực hiện lệnh ping trong vòng 5s (mặc định sẽ gửi được 5 gói tin):

`ping google.com –w 5`

<img src = "http://imgur.com/le4zr0T.jpg">

### 6) Đặt time to live cho gói tin gửi đi:

<img src = "http://imgur.com/p7EmG8B.jpg">

### 7) Tùy chọn -r :

<img src = "http://imgur.com/Bg1qPBp.jpg">

<a name = "2"></a>
# 2. Lệnh fping

<a name = "2.1"></a>
## 2.1. Giới thiệu

-	**fping** là một chương trình gửi các gói tin ICMP echo probe tới các host trong mạng, giống như **ping**, nhưng thực hiện tốt hơn khi ***có thể ping tới nhiều host cùng lúc***.

-	fping khác ping là có thể xác định số đích trong cùng một dòng lệnh, xác định một file chứa các địa chỉ của host để ping. Thay vì gửi từng gói tin và chờ cho đến khi có gói tin reply trả về mới ping tiếp, fping sẽ gửi ra một gói tin và đi vòng.

-	Ở chế độ mặc định, nếu có một địa chỉ reply lại thì nó sẽ note lại và loại khỏi danh sách các địa chỉ cần ping để check. Nếu không có reply trong vòng một thời gian nhất định nó sẽ note lại là không tìm thấy (unreachable)

-	fping cũng hỗ trợ gửi một số lượng ping nhất định tới host, hoặc lặp vô hạn như ping.

-	Không giống như ping, fping được sử dụng trong scripts, do đó đầu ra của nó được thiết kế để dễ dàng phân tích.


-	fping sử dụng cho Ipv4.

-	fping không được hỗ trợ sẵn như ping nên bạn cần download fping bằng câu lệnh: 

`apt-get install fping`

- Cấu trúc câu lệnh fping: 

`fping [ options ] [ systems... ]`

<a name = "2.2"></a>
## 2.2. Một số tùy chọn

\- **-a** : Show ra thông tin xem host còn hoạt động hay không.

\- **-A** : Show ra địa chỉ IP của host hơn là ánh xạ ra tên miền.

\- **-b** *number* : set số byte dữ liệu trong phần dữ liệu ICMP để ping. Giống tùy chọn **–s** của `ping`.

\- **-c** *number*: Xác định số gói tin ICMP gửi đi trước khi kết thúc lệnh ping.

\- **-C** *number*: Giống –c nhưng thống kê thông tin thời gian gửi các gói tin đến cùng một host để phân tích.

\- **-d** : Sử dụng để ánh xạ ra tên miền của host.

\- **-e** : Hiển thị thông tin thời gian gửi gói tin round-trip-time (Nếu gửi nhiều gói tin ping thì không cần tùy chọn **–e**)

\- **-f** *file_name*: Đọccác địa chỉ host cần ping từ một file. Tùy chọn này chỉ được sử dụng bởi người dùng root. Những người dùng thường thì sử dụng thông qua stdin như sau:

`fping < targets_file `

\- **-g** *addr/mask* : Sinh ra một list các địa chỉ đích nằm trong dải mạng đưa ra, hoặc từ địa chỉ bắt đầu đến địa chỉ kết thúc của dải đã cho.

 Ví dụ: `fping –g 10.10.10.0/24` hoặc `fping –g 10.10.10.1 10.10.10.100`


\- **-i** *time* : Xác định thời gian tối thiểu (tính theo ms) gửi giữa 2 gói tin ping tới bất kì host nào. (mặc định là 25)

\- **-l** : gửi ping vô thời hạn cho đến khi nhấn CTRL + C để dừng lại.

\- **-q** : không hiển thị thông tin ra màn hình, chỉ hiển thị kết quả tóm tắt cuối cùng.

\- **-Q** *time* : giống –q nhưng hiển thì thông tin tóm tắt sau mỗi time giây.

\- **-s** : thống kê lại thông tin lại cho đến khi dừng lại. 

\- **-S** *addr*: chỉ định giá trị source address cho gói tin gửi đi.

\- **-I** *if_name* : chỉ định interface dùng để gửi bản tin icmp.

\- **-u** : Hiển thị ra những host unreachable 

\- **-H** *number* : set time-to-live cho gói tin.

Các tùy chọn khác tham khảo thêm tại [manpage fping](http://manpages.ubuntu.com/manpages/xenial/man8/fping.8.html)


<a name = "2.3"></a>
## 2.3. Một số ví dụ

### 1) Gửi 3 lần  ping tới 3 địa chỉ google.com, facebook.com, 8.8.8.8 thì dừng lại:

<img src = "http://imgur.com/EPIPovo.jpg">

### 2) Ping đến các host được lưu trong file targets_file cho trước: 

<img src = "http://imgur.com/x0RCyD3.jpg">

### 3) Ping đến các địa chỉ trong một dải địa chỉ đưa ra với tùy chọn –g  trong dải địa chỉ đưa ra từ 10.10.10.1 tới 10.10.10.6 và hiển thị ra các host unreachable:

<img src = "http://imgur.com/q72sTNu.jpg">

### 4) Sử dụng tùy chọn –g, –s và –q để hiển thị thông tin số host đang hoạt động trong một mạng: 

<img src = "http://imgur.com/st7wSxc.jpg">

### 5) Dùng tùy chọn –S để đổi địa chỉ nguồn gửi gói tin ICMP và đặt TTL cho gói tin là 1: 

<img src = "http://imgur.com/sBWvSyv.jpg">

Phân tích trên wireshark ta được như sau:

<img src = "http://imgur.com/4MJ1SMO.jpg">


<a name = "3"></a>
# 3. Tham khảo

http://manpages.ubuntu.com/manpages/xenial/man8/fping.8.html

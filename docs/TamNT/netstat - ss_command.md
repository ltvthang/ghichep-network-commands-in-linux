# netstat and ss command

## ***Mục lục***

[1. Lệnh netstat](#1)

- [1.1. Giới thiệu lệnh netstat](#1.1)

- [1.2. Cấu trúc câu lệnh và một số tùy chọn của netstat](#1.2)

- [1.3. Một số ví dụ](#1.3)

[2. Lệnh ss](#2)

- [2.1. Giới thiệu](#2.1)

- [2.2. Cấu trúc câu lệnh và một số tùy chọn](#2.2)

- [2.3. Một số ví dụ](#2.3)


[3. Tham khảo](#3)

---

<a name = "1"></a>
# 1. Lệnh netstat 

<a name = "1.1"></a>
## 1.1. Giới thiệu lệnh netstat


- **netstat (network statistics)** là một công cụ dòng lệnh dùng để ***theo dõi các kết nối mạng*** cả kết nối đến và đi cũng như là ***xem các bảng định tuyến***, ***thống kê*** các interface… netstat có sẵn trên hầu hết các hệ điều hành like-Unix và cũng làm việc tốt trên Window OS. 

- Nó rất hữu ích trong việc phát hiện và xử lý sự cố mạng cũng như xác định lưu lượng trong mạng để đo đạc hiệu suất hoạt động của mạng. 

- **netstat** là một trong những công cụ debug lỗi mạng cơ bản và hiệu quả nhất, cho biết những cổng nào đang mở và cổng mà bất kì chương trình nào đang dùng để lắng nghe.

<a name = "1.2"></a>
## 1.2. Cấu trúc câu lệnh và một số tùy chọn của netstat

### Cấu trúc câu lệnh như sau:

```
netstat  [address_family_options]  [--tcp|-t]   [--udp|-u]   [--raw|-w]
  [--listening|-l]     [--all|-a]     [--numeric|-n]    [--numeric-hosts]
       [--numeric-ports]           [--numeric-users]           [--symbolic|-N]
       [--extend|-e[--extend|-e]]  [--timers|-o] [--program|-p] [--verbose|-v]
       [--continuous|-c]
```

```   
netstat {--route|-r} [address_family_options]
       [--extend|-e[--extend|-e]] [--verbose|-v] [--numeric|-n]
       [--numeric-hosts] [--numeric-ports] [--numeric-users] [--continuous|-c]
``` 

```     
netstat   {--interfaces|-i}    [--all|-a]    [--extend|-e[--extend|-e]]
       [--verbose|-v]    [--program|-p]    [--numeric|-n]    [--numeric-hosts]
       [--numeric-ports] [--numeric-users] [--continuous|-c]
``` 

```    
   netstat      {--groups|-g}       [--numeric|-n]       [--numeric-hosts]
       [--numeric-ports] [--numeric-users] [--continuous|-c]
``` 

```       
 netstat       {--masquerade|-M}       [--extend|-e]      [--numeric|-n]
       [--numeric-hosts] [--numeric-ports] [--numeric-users] [--continuous|-c]
``` 

```     
  netstat {--statistics|-s} [--tcp|-t] [--udp|-u] [--raw|-w]
``` 

```      
 netstat {--version|-V}
``` 
  
 `netstat {--help|-h}`
      
Trong đó,  `address_family_options` là: 

``` 
       [-4]      [-6]       [--protocol={inet,unix,ipx,ax25,netrom,ddp}[,...]]
       [--unix|-x] [--inet|--ip] [--ax25] [--ipx] [--netrom] [--ddp]
``` 

### Một số tùy chọn:

  **--route , -r**  :  Hiển thị bảng định tuyến của kernel 

   **--groups , -g**:  Hiển thị các thành viên trong địa chỉ multicast Ipv4 và Ipv6

   **--interfaces, -i**:  Hiển thị tất cả các interface.


   **--statistics , -s**: Thống kê tóm tăt tất cả các kết nối. 

   **--numeric , -n** :   Hiển thị địa chỉ theo số thay vì hiển thị tên.(Khi sử dụng –n , tất cả địa chỉ host, cổng và tên người dùng đều hiển thị số)
 
   **--numeric-hosts** :  Hiển thị địa chỉ của host nhưng không ảnh hưởng tới sự phân giải tên cổng và tên người dùng.

   **--numeric-ports** : Hiển thị địa chỉ port dạng số, không ảnh hưởng tới sự phân giải tên địa chỉ host và tên người dùng. 

   **--numeric-users** :  Hiển thị tên người dùng dạng ID, không ảnh hưởng tới sự phân giải tên địa chỉ host và tên cổng. 

   **--protocol** = *family* , **-A**:  Xác định kiểu  địa chỉ *family* của kết nối được show ra. Bao gồm các giá trị: inet, unix, ipx, ax25, netrom, và ddp. Bao gồm cả các kiểu raw, udp và tcp protocol sockets.

   **-c, --continuous** *[time]* : Tùy chọn để netstat in ra thông tin sau mỗi bao nhiêu giây tương ứng.

   **-e, --extend**: Hiển thị thêm thông tin. 

   **-o, --timers** : Hiển thị thông  tin bao gồm cả thời gian hoạt động của mạng. 

   **-p, --program** : HIển thị ra số hiệu PID và tên chương trình mà socket thuộc về. 

   **-l, --listening** : Chỉ hiển thị những socket đang lắng nghe.

   **-a, --all** :  Hiển thị tất cả các socket dù có đang lắng nghe hay không. Với tùy chọn  --interface, sẽ show ra taats cả các interface không bật.


   **-C** :  In ra thông tin định tuyến trong bảng định tuyến cache. 


Tham khảo thêm các tùy chọn khác tại [manpage netstat](http://manpages.ubuntu.com/manpages/trusty/man8/netstat.8.html)

<a name = "1.3"></a>
## 1.3. Một số ví dụ

### 1)  Hiển thị tất cả các socket có trong máy, cả các socket đang lắng nghe và các socket chưa kết nối:

`netstat –a`


<img src = "http://imgur.com/y5ot355.jpg">

### 2) Hiển thị ra các kết nối tcp đang lắng nghe, hiển thị thêm cả thời gian và người dùng đang dùng kết nối đó

`netstat –lo -t -e` hoặc `netstat -lteo`


<img src = "http://imgur.com/mdKms8H.jpg">

### 3) Hiển thị ra các kết nối đang dùng udp, hiển thị thông tin tên người dùng dạng UID và tên chương trình đang sử dụng kết nối đó:

`netstat –luep –numeric-users` 


<img src = "http://imgur.com/c7O9mEU.jpg">

### 4)  Hiển thị thông tin trong bảng định tuyến: 

`netstat –r` 


<img src = "http://imgur.com/Ih5yXZ6.jpg">

### 5) Hiển thị thông tin các interface sử dụng trong máy với tùy chọn **–i** (các interface đang bật). kết hợp thêm tùy chọn **–e** ta được thông tin như gõ lệnh `ifconfig`

<img src = "http://imgur.com/1Jcp015.jpg">

### 6) Kiểm tra xem dịch vụ dịch vụ dhcp trên máy chủ có đang sử dụng hay không sử dụng netstat kết hợp grep:

`netstat –lep | grep :dhcp`


<img src = "http://imgur.com/fskpTpr.jpg">


<a name = "2"></a>
# 2. Câu lệnh ss

<a name = "2.1"></a>
## 2.1. Giới thiệu

-	Bên trên, chúng ta đã tìm hiểu lệnh netstat, nhưng từ lâu, nó đã trở nên lạc hậu và dần được thay thế bằng lệnh ss trong bộ công cụ iproute2. 

-	Lệnh ss có khả năng hiển thị nhiều thông tin hơn netstat và nhanh hơn. Lệnh netstat đọc nhiều file trong thư mục tiến trình  `/proc` để thu thập thông tin. Tuy nhiên phương pháp này sẽ trở nên hạn chế khi có quá nhiều kết nối để hiển thị. Điều này làm cho nó chậm hơn.

-	Lệnh ss lấy thông tin **trực tiếp từ kernel**. Những tùy chọn được sử dụng với ss tương đối giống với netstat – điều này làm cho nó dễ dàng thay thế được netstat. 

-	Hầu hết các bản phân phối của Linux đều đã hỗ trợ nhiều công cụ theo dõi trong đó có cả ss nên bạn không cần cài đặt.

-	ss giống như netstat, được sử dụng để hiển thị thông tin thống kê socket. Nó có thể hiển thị cho PACKET socket, TCP socket, UDP socket, RAW socket, Unix domain socket, …

<a name = "2.2"></a>
## 2.2. Cấu trúc câu lệnh và một số tùy chọn

-	Cấu trúc câu lệnh: 

`ss [options] [ FILTER ]`

-	Các tùy chọn: 

  \-	Khi không có tùy chọn nào được sử dụng, ss hiển thị danh sách các socket không mở cho kết nối TCP mà đã được thiết lập.

  \-	Các tùy chọn hầu như gần giống với lệnh netstat. Tham khảo thêm tại [man page netstat](http://manpages.ubuntu.com/manpages/trusty/man8/netstat.8.html).

  \-	Tuy nhiên, ss cho phép thêm tính năng ưu việt hơn đó là lọc dữ liệu dựa trên thông tin list các socket. Do đó, ta có thể lọc dữ liệu dựa trên state, address và port ở đầu ra. 

- Cấu trúc FILTER như sau: 

`FILTER := [ state TCP-STATE ] [ EXPRESSION ]`

-	ss cho phép lọc các socket theo trạng thái sử dụng keyword **state** hoặc **exclude**, lọc theo tên các state của socket.

  -  **Lọc theo trạng thái socket**

      Một số định danh cho các trạng thái của socket như: 
      
      - Tất cả các trạng thái chuẩn của kết nối TCP như: ***established, syn-sent, syn-recv, fin-wait-1, fin-wait-2, time-wait, closed, close-wait, last-ack, listening*** và ***closing***.
      
      - ***all*** : tất cả các loại state.
      
      - ***connected***: tất cả các state ngoại trừ state listen và close.
      
      - ***aynchronized*** : tất các trạng thái connected ngoại trừ syn-sent
      
      - ***bucket***: các trạng thái duy được duy trì như các minisocket. (ví dụ: time-wait và syn-recv)
      
      - ***big***: trái ngược với bugket
      
      Ví dụ để hiển thị các socket đang trong trạng thái không phải là SYN-SENT:
      
      `ss exclude SYN-RECV`
      
      Các trạng thái khác xem thêm ở phần State trong manpage netstat. 

  - **Lọc theo địa chỉ và cổng** : Có thể lọc theo các loại sau
  
    - Lọc theo địa chỉ: 

    ```
        dst prefix:port
        src prefix:port
        src unix:STRING
        src link:protocol:ifindex
        src nl:channel:pid
    ```

    Trong đó, cả địa chỉ **prefix** và **port** đều có thể thay bằng kí tự đại diện * để đại diện cho tất cả các giá trị. Địa chỉ cũng có thể thay bằng tên ánh xạ DNS. Trong đó: **src** là địa chỉ nguồn, **dst** là địa chỉ đích.

    - Lọc theo cổng: có thể kết hợp số cổng với các toán tử <, >, =, >=, =, ==, !=, eq, ge, lt, ne... để lọc. 

    Ví dụ như: 

    ```     
      dport >= :1024
      dport != :22
      sport < :32000
    ```

    (với **sport** là cổng nguồn, **dport** là cổng đích)

Tham khảo các ví dụ sau để hiểu rõ hơn về filter socket dùng ss.

<a name = "2.3"></a>
## 2.3. Một số ví dụ

Vì `ss` có các tùy chọn tương đối giống `netstat` nên phần này sẽ chỉ nêu một số tùy chọn với tính năng lọc ưu việt của `ss`.

### 1) Hiển thị các kết nối hoạt động ở cổng http 

`ss –atopn src * :http   #Hiển thị kết nối tcp, địa chỉ và cổng hiện dạng số, hiển thị tên và người dùng đang sử dụng chương trình`


<img src = "http://imgur.com/B80s5b1.jpg">


### 2) Hiển thị các socket đang có kết nối ở trạng thái LISTEN 

`ss –aep state listening `


<img src = "http://imgur.com/iRV1i1M.jpg">


### 3) Hiển thị xem máy có đang chạy chương trình ssh hay không: 

`ss state established  sport = :22`


<img src = "http://imgur.com/OTmJpo4.jpg">


### 4) Hiển thị các socket tcp hoạt động trên dải địa chỉ private của máy – dải 10.10.10.0/24:


<img src = "http://imgur.com/kpRj2yo.jpg">


### 5) Hiển thị các chương trình đang chạy trên các cổng trong phạm vi từ 20 tới 70: 


<img src = "http://imgur.com/OLM90of.jpg">


###  6) Lọc các socket theo trạng thái sử dụng keyword `exclude`: 

<img src = "http://imgur.com/uTVlDN9.jpg">


### ***Lưu ý:***

\- Khi thực hiện lọc, nên thêm các tùy chọn loại kết nối (như –t cho tcp, -u cho udp ) để dễ dàng lấy được kết quả mong muốn. Nếu chỉ sử dụng tùy chọn –a thì khi đó, kết quả sẽ trả về các kết nối nội bộ trong máy mà mình chưa có khả năng hiểu rõ hết. Do kiến thức mình còn hạn chế nên chưa hiểu rõ cách thức lọc thực sự của ss nên tạm thời dùng thêm tùy chọn –t và –u để dễ dàng sử dụng. 

\- Theo cá nhân mình thì phần lọc filter này  của `ss` kiểu như là cách kết hợp 2 lệnh `netstat` và `grep`. 


<a name = "3"></a>
# 3. Tham khảo

[1] Man page netstat : http://manpages.ubuntu.com/manpages/trusty/man8/netstat.8.html

[2] Man page ss: http://manpages.ubuntu.com/manpages/trusty/man8/ss.8.html

[3] ss filter: https://www.apt-browse.org/browse/ubuntu/trusty/main/all/iproute2-doc/3.12.0-2/file/usr/share/doc/iproute2-doc/ss.html

[4] Một số ví dụ về ss: https://www.cyberciti.biz/tips/linux-investigate-sockets-network-connections.html
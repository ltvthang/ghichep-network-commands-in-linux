# curl command

## ***Mục lục***

[1. Giới thiệu](#1)

- [1.1. Giới thiệu về lệnh curl](#1.1)

- [1.2. Cấu trúc câu lệnh curl](#1.2)

[2. Một số ví dụ với curl](#2)

[3. Tham khảo](#3)

---

<a name = "1"></a>
# 1. Giới thiệu 

<a name = "1.1"></a>
## 1.1. Giới thiệu về lệnh curl

-	**`curl`** là một công cụ để truyền dữ liệu về hoặc đến một server, được sử dụng và hỗ trợ nhiều giao thức như (DICT, FILE, FTP, FTPS, GOPHER, HTTP, HTTPS,  IMAP, MAPS,  LDAP,  LDAPS,  POP3, POP3S, RTMP, RTSP, SCP, SFTP, SMTP, SMTPS, TELNET and TFTP).

-	Câu lệnh được thiết kế để làm việc mà không cần sự tương tác của người dùng.

-	Curl cung cấp một loạt các thủ thuật hữu ích như hỗ trợ proxy, xác thực người dùng, upload FTP, HTTP post, kết nối SSL, cookies, file transfer resume, metalink và nhiều hơn nữa. 

-	Curl cố gắng sử dụng lại các kết nối khi truyền nhiều file, hoặc lấy các file từ cũng server để không tạo thêm nhiều kết nối hoặc các bước handshake. Điều này làm cải thiện tốc độ. 

-	Một thuận lợi lớn nhất mà hàm curl này mang lại đó là tốc độ, nhanh hơn rất nhiều so với hàm open file. cURL được ví như một công cụ giao tiếp đa giao thức, giúp ta xem hoặc tải một địa chỉ.

-	Curl thường hiển thị các thông số của dữ liệu trong quá trình xử lý như: các dữ liệu truyền, tốc độ, thời gian truyền, …

<a name = "1.2"></a>
## 1.2. Cấu trúc câu lệnh curl

```curl [options] [URL...]```



Trong đó, một số tùy chọn cần biết như sau:

- **-C, --continue-at <offset>**: Tiếp tục phiên truyền trước đó với offset được đưa ra. **offset** được đưa ra là số byte chính xác mà phiên truyền curl đang dừng lại. Sử dụng trong trường hợp upload dữ liệu. 

  Sử dụng "-C -" để curl tự động tiếp tục trở lại phiên truyền đang bị dừng lại do vô tình hoặc cố ý trước đó.
              
- **--interface <name>** Chỉ định sử dụng interface nào cho curl. (bạn có thể để là interface name, địa chỉ IP hoặc host name tùy ý).

  Ví dụ: ` curl --interface eth0 http://www.netscape.com/`

- **-L, --location** (sử dụng với HTTP/HTTPs) Nếu server trả lại request của client là server đã di chuyển sang địa điểm khác. Sử dụng tùy chọn -L để nó tự biết chuyển sang địa điểm mới.
              
- **--limit-rate <speed>** : Xác định tốc độ tối đa mà bạn muốn curl sử dụng. Đặc tính này sẽ hữu ích để bạn có thể quản lý băng thông của mình.

- **-m, --max-time <seconds>** Xác định số thời gian tối đa bạn cho phép thực hiện truyền dữ liệu trong curl. Tương tự như --connetc-timeout.


- **--mail-from <address>** và **--mail-rcpt <address>** sử dụng trong giao thức gửi mail SMTP.

- **--max-filesize <bytes>** Giới hạn kích thước file tối đa truyền curl.

- **-o, --output <file>** Viết đầu ra được trả về vào một file tên <file> thay vì trả về tại đầu ra stdout. 

- **-O, --remote-name** Lưu lại đầu ra vào file tên giữ nguyên như trên server. 

- **-T, --upload-file <file>** dùng upload file.

- **-z, --time-cond <date expression>|<file>** request một file chỉnh sửa được xác định sau thời điểm time và date được đưa ra, hoặc có thể hoặc trước thời điểm time. 

Các options khác của câu lệnh tham khảo tại [manpage curl](http://manpages.ubuntu.com/manpages/trusty/man1/curl.1.html)            

<a name = "2"></a>
# 2. Một số ví dụ với curl

## 2.1. Lấy dữ liệu và lưu vào một file tên test.txt:

```
ttp@ubuntuserver:~$ curl -o test.txt https://raw.githubusercontent.com/ThanhTamPotter/thuctap012017/master/TamNT/README.md
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100    52  100    52    0     0     70      0 --:--:-- --:--:-- --:--:--    70
```


## 2.2. Lấy dữ liệu và lưu file dưới tên của chính nó: 

`curl -O https://raw.githubusercontent.com/ThanhTamPotter/thuctap012017/master/TamNT/README.md`

<img src = "http://imgur.com/0noewD4.jpg">

## 2.3. Lấy dữ liệu về lưu vào file tên 1 và giới hạn kích thước file là 10KB, liên kết mạng thông qua card mạng eth0: 

<img src = "http://imgur.com/F6R2gxn.jpg">

## 2.4. Gửi mail sử dụng giao thức SMTP:

`curl --mail-from blah@test.com --mail-rcpt foo@test.com smtp://mailserver.com`

## 2.5. Upload file đến FTP server  sử dụng tùy chọn –T:

`curl –u ftpuser:ftppass –T file_name ftp://ftpserver_address`

<img src = "http://imgur.com/QpcLwTz.jpg">

## 2.6. Hạn chế tốc độ download bằng tùy chọn –limit-rate và lấy về các file có sự thay đổi trước khoảng thời gian 23/3/17:

`curl https://raw.githubusercontent.com/ThanhTamPotter/thuctap012017/master/TamNT/Wordpress.md -O --limit-rate 1M -z 23-March-17`

<img src = "http://imgur.com/eyx972B.jpg">

<a name = "3"></a>
# 3. Tham khảo

[1] curl manpage: http://manpages.ubuntu.com/manpages/trusty/man1/curl.1.html

[2] Một số ví dụ: http://www.thegeekstuff.com/2012/04/curl-examples/?utm_source=feedburner
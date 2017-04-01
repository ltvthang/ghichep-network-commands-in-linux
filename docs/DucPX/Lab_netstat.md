# Tìm hiểu về lệnh `Netstat`

## 1. Lệnh netstat để làm gì?

#### Netstat (Network statistics) là lệnh dùng để hiện thị các thông tin khác nhau liên quan đến network như là các kết nối mạng, bảng định tuyến, liệt kê các interface, etc.

## 2. Một số tùy chọn của netstat

### 2.1 Liệt kê tất cả các port (cả port đang lắng nghe và không lắng nghe): `netstat -a | more`

![Imgur](http://i.imgur.com/UWUHMcz.png)

- 2.1.1 Liệt kê tất cả tcp port `netstat -at`

![Imgur](http://i.imgur.com/ZCOuPc3.png)

- 2.1.2 Liệt kê tất cả udp port `netstat -au`

![Imgur](http://i.imgur.com/yDRxeHt.png)

### 2.2 Liệt kê tất cả Sockets đang trong trạng thái lắng nghe `netstat -l`

![Imgur](http://i.imgur.com/57Kcmmp.png)

- 2.2.1 Liệt kê chỉ các cổng tcp đang lắng nghe `netstat -lt`

![Imgur](http://i.imgur.com/rlqYQ6D.png)

- 2.2.2 Liệt kê chỉ các cổng udp đang lắng nghe `netstat -lu`

![Imgur](http://i.imgur.com/JBLDZgG.png)

### 2.3 Hiện thị theo từng giao thức `netstat -s`
![Imgur](http://i.imgur.com/MY6kujs.png)

- hiện thị theo giao thức tcp: `netstat -st`
- hiện thị theo giao thức udp: `netstat -su`

### 2.4 Hiện thị PID và tên chương trình `netstat -p`

### 2.5 Hiện thị thông tin bảng định tuyến `netstat -r`

![Imgur](http://i.imgur.com/fv5P20B.png)

### 2.6 Hiện thị danh sách interface `netstat -i`
![Imgur](http://i.imgur.com/kdS1rzw.png)

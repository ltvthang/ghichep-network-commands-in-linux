# Lệnh SS

## Giới thiệu
- SS (socket statistics) tương tự như netstat dùng để thống kê các kết nối mạng. Nhưng SS có khả năng hiện thị thông tin nhiều hơn và nhanh hơn so với netstat.
- Câu lệnh ss nhận các thông tin về socket statistics một cách trực tiếp từ nhân hệ điều hành. Các tùy chọn đi kèm với ss command thì đơn giản hơn so với netstat khiến ss command có thể thay thế cho netstat một cách dễ dàng

## Một số ví dụ về lệnh SS
- 1. Liệt kê tất cả các cổng `ss | less`

![Imgur](http://i.imgur.com/KtfgxZm.png)

- 2. Lọc kết nối tcp, udp hoặc unix
	- 2.1 lọc kết nối tcp: `ss -t` (chỉ các cổng đang kết nối tcp)
	
	![Imgur](http://i.imgur.com/JhrLaTE.png)
	
	- 2.2 để liệt kê ra tất cả các cổng đang kết nối và không kết nối: `ss -t -a` 
	
	![Imgur](http://i.imgur.com/MkBZeMS.png) 

	- 2.3 tương tự như tcp, với udp ta thay tùy chọn **-t** bằng **-u**
	
	![Imgur](http://i.imgur.com/V9iiZpg.png)

	![Imgur](http://i.imgur.com/V9iiZpg.png)

	- 2.4 với unix thì tùy chọn là **-x**

	![Imgur](http://i.imgur.com/QVDqY0k.png)

- 3. liệt kê tât cả các cổng đang listen

![Imgur](http://i.imgur.com/rd2dlmT.png)

- 4. liệt tất cả các cổng đang kết nối (hiện thị số cổng, không hiện thị tên)

![Imgur](http://i.imgur.com/q0p4qRp.png)

- 5. In ra tổng thống kê tổng các port

![Imgur](http://i.imgur.com/zco8g7I.png)

- 6. Liệt kê các kết nối ipv4 và ipv6
	- ipv4 dùng tùy chọn `-f inet` hoặc `-4`
	
![Imgur](http://i.imgur.com/kchAgZF.png)

	- ipv6 tùy chọn `-f inet6` hoặc `-6`

- 7. Hiện thị bộ đếm thời gian kết nối `-o`

![Imgur](http://i.imgur.com/fE7QfBe.png)

- 8. Hiện thị tên tiến trình và pid `-p`

![Imgur](http://i.imgur.com/qOLrdEy.png)

---
#### Trên đây là một số tiện ích của lệnh SS trong linux. 
# Thực hành lệnh IP trên Ubuntu Server 14.04 - 64 bit


## 1. Cấu hình địa chỉ IPv4 tĩnh
- Sửa trong file cấu hình mạng `/etc/network/interfaces`
- Để cấu hình địa chỉ IP tĩnh cho card mạng eth0, ta thay đổi nội dung trong file cấu hình như sau ![Imgur](http://i.imgur.com/UDIGqJy.png)
	- IP address: 172.16.69.10
	- netmask: 255.255.255.0
	- gateway: 172.16.69.1
	- dns-nameservers: 8.8.8.8
	
- `sudo ifdown eth0 && sudo ifup eth0` để card eth0 nhận thông tin cấu hình mới

## 2. Gán địa chỉ IP cho một interface card xác định
gán một địa chỉ IP cho một card mạng nào đó. Địa chỉ sẽ bị mất khi máy khởi động lại.

`ip addr add 10.10.20.10/24 dev eth2`

## 3. Xóa 1 địa chỉ IP
`ip addr del 10.10.20.10/24 dev eth2`

## 4. Show thông tin cấu hình của tất cả card mạng.

`ip addr show`

![Imgur](http://i.imgur.com/KWeNoIa.png)

## 5. Enable, disable 1 interface
- enable: `ip link set eth2 up`
- disable: `ip link set eth2 down`

## 6. Xem bảng định tuyến
`ip route show`

![Imgur](http://i.imgur.com/fNdjEBE.png)

## 7. Thêm một đường đi tĩnh

`sudo ip route add [địa chỉ mạng cần tới] via [địa chỉ sẽ đi qua] dev [interface sẽ đi qua]`

ví dụ: cần tới mạng `10.10.20.0/24` thông qua interface eth2 có địa chỉ `10.10.20.10` như sau:

`sudo ip route add 10.10.20.0/24 via 10.10.20.10 dev eth2` 

Chúng ta có thể định nghĩa đường đi tĩnh này trong file `/etc/network/interfaces` với dòng cấu hình: `up ip route add 10.10.20.0/24 via 10.10.20.10 dev eth2`

## 8. Remove một đường tĩnh

`sudo ip route del [địa chỉ mạng cần xóa]`. 

ví dụ: `sudo ip route del 10.10.20.0/24`


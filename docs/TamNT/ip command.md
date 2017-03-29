# ip command

## ***Mục lục***

[1. Câu lệnh ip ](#1)

[2. Câu lệnh ip link](#2)

- [2.1. Giới thiệu và cấu trúc câu lệnh chung](#2.1)

- [2.2. Một số ví dụ](#2.2)

[3. Câu lệnh ip address](#3)

- [3.1. Giới thiệu và cấu trúc câu lệnh](#3.2)

- [3.2. Một số ví dụ với ip address](#3.2)

[4. Câu lệnh ip route](#4)

- [4.1. Giới thiệu](#4.1)

- [4.2. Cấu trúc câu lệnh](#4.2)

- [4.3. Một số ví dụ với ip route](#4.3)

[5. Tham khảo](#5)

---

<a name = "1"></a>
# 1. Câu lệnh ip

Lệnh `ip` cũng tương tự như `ifconfig` nhưng có mạnh mẽ hơn và hoàn toàn có thể dùng để thay thế nó. Với `ip`, bạn có thể dễ dàng trong việc quản trị mạng và chỉ với một câu lệnh.

- Cấu trúc chung của câu lệnh như sau:

`ip [ OPTIONS ] OBJECT { COMMAND | help }`

Trong đó: 
```
       OBJECT := { link | address | addrlabel | route | rule | neigh | ntable
               | tunnel | tuntap | maddress | mroute | mrule | monitor | xfrm
               | netns | l2tp | tcp_metrics }
```

```
       OPTIONS := { -V[ersion] | -h[uman-readable] | -s[tatistics] |
               -r[esolve] | -f[amily] { inet | inet6 | ipx | dnet | link } |
               -o[neline] | -n[etns] name | -a[ll] | -c[olor] }
```

Tham khảo thêm định nghĩa các thành phần tại [manpage ip](http://manpages.ubuntu.com/manpages/xenial/en/man8/ip.8.html)

***Chú ý***: Tất cả các đối tượng phần OBJECT đều có thể viết dưới dạng đầy đủ hoặc viết tắt, hệ thống linux có thể hiểu được.

Ví dụ: 

\- `ip address` <=> `ip addr` <=> `ip a`

\- `ip link` <=> `ip l`

\- `ip route` <=> `ip r`

Sau đây sẽ tìm hiểu một số lệnh ip với các object thông dụng: `ip link`, `ip address`, `ip route`, …

<a name ="2"></a>
# 2. Câu lệnh ip link

<a name = "2.1"></a>
## 2.1. Giới thiệu và cấu trúc câu lệnh chung

- Câu lệnh cấu hình thiết bị mạng.

- Là một phần của **iproute2**, `ip link` cung cấp khả năng mô tả thông tin lớp link layer, kích hoạt hoặc tắt một interface, thay đổi trạng thái link layer, thay đổi MTU, tên interface và thậm chí là địa chỉ phần cứng và địa chỉ broadcast lớp 2.

- Cấu trúc chung:

```
ip [ OPTIONS ] link  { COMMAND | help }

OPTIONS := { -V[ersion] | -h[uman-readable] | -s[tatistics] |
               -r[esolve] | -f[amily] { inet | inet6 | ipx | dnet | link } |
               -o[neline] | -br[ief] }



TYPE := [ bridge | bond | can | dummy | hsr | ifb | ipoib | macvlan |
               macvtap | vcan | veth | vlan | vxlan | ip6tnl | ipip | sit |
               gre | gretap | ip6gre | ip6gretap | vti | nlmon | ipvlan |
               lowpan | geneve ]

```

Hiểu rõ các thành phần trong OPTIONS và TYPE tại [manpage ip link](http://manpages.ubuntu.com/manpages/xenial/en/man8/ip-link.8.html)

<a name = "2.2"></a>
## 2.2. Một số ví dụ với `ip link`

- **`ip link show`: Show thông tin các thiết bị mạng**

  \- Cú pháp : `ip link show [ DEVICE | group GROUP | up | master DEVICE | type TYPE ]`

  \- Một số ví dụ:

      -	Show ra các thông tin các thiết bị:

      `ip link show`

      -	Show ra các thiết bị đang up:

      `ip link show up`

      -	Show ra thông tin các thiết bị trong nhóm 1:

      `ip link show group default`

<img src ="http://imgur.com/cUpaACJ.jpg">


- **`ip link add`: add thêm các thiết bị ảo trong hệ thống linux**

  \- Cú pháp:

  ```
  ip link add [ link DEVICE ] [ name ] NAME
               [ txqueuelen PACKETS ]
               [ address LLADDR ] [ broadcast LLADDR ]
               [ mtu MTU ] [ index IDX ]
               [ numtxqueues QUEUE_COUNT ] [ numrxqueues QUEUE_COUNT ]
               type TYPE [ ARGS ]

   TYPE := [ bridge | bond | can | dummy | hsr | ifb | ipoib | macvlan |
               macvtap | vcan | veth | vlan | vxlan | ip6tnl | ipip | sit |
               gre | gretap | ip6gre | ip6gretap | vti | nlmon | ipvlan |
               lowpan | geneve ]
  ```

  \- Ví dụ: 

  -	Thêm một card ảo vlan 20 trên card thật eth1:

  `ip link add link eth1 vlan20 type vlan id 20`


  -	Thêm một interface bridge:

  `ip link add brtest type bridge`

<img src ="http://imgur.com/9Joxcgt.jpg">

- **`ip link delete`: delete virtual link**

  \- Cấu trúc câu lệnh:  `ip link delete { DEVICE | group GROUP } type TYPE [ ARGS ]`

  Trong đó: 

	```
		dev DEVICE
              specifies the virtual device to act operate on.

       group GROUP
              specifies the group of virtual links to delete. Group 0 is not
              allowed to be deleted since it is the default group.

       type TYPE
              specifies the type of the device.
	```
  \- Ví dụ:	Xóa bridge vừa tạo: 

	`ip link delete brtest`

	`ip link delete vlan20`

<img src ="http://imgur.com/8dT2InO.jpg">

- **`ip link set`: Thay đổi thông số thiết bị**

Một số ví dụ: 

  -	Thay đổi địa chỉ MAC của các card ảo vlan10:

  `ip link set vlan10 address 00:0c:9d:29:dc:30`

  -	Đổi tên card vlan10 thành vlan100:

  `ip link set vlan10 name vlan100`

  -	Tắt card eth1:

  `ip link set eth1 down`

  -	Set MTU của eth1 là 2000 byte: 

  `ip link set eth1 mtu 2000`

<img src ="http://imgur.com/HWfcm7C.jpg">


<a name = "3"></a>
# 3. Câu lệnh `ip address`

<a name = "3.1"></a>
## 3.1. Giới thiệu và cấu trúc chung câu lệnh ip address

- Câu lệnh quản lý ip address.

- Là một phần của **iproute2**, `ip address` có thể liệt kê các địa chỉ IP gán với các interfaces, thêm, xóa hoặc xóa toàn bộ địa chỉ IP của một thiết bị đưa ra.

- Cấu trúc chung câu lệnh: 

```
 ip [ OPTIONS ] address  { COMMAND | help }

       ip address { add | change | replace } IFADDR dev IFNAME [ LIFETIME ] [
               CONFFLAG-LIST ]

       ip address del IFADDR dev IFNAME [ mngtmpaddr ]

       ip address { show | save | flush } [ dev IFNAME ] [ scope SCOPE-ID ] [
               to PREFIX ] [ FLAG-LIST ] [ label PATTERN ] [ up ]

       ip address { showdump | restore }
```

Tham khảo thêm các thông số tùy chọn tại [manpage ip address](http://manpages.ubuntu.com/manpages/xenial/en/man8/ip-address.8.html)

<a name = "3.2"></a>
## 3.2. Một số ví dụ với ip address

- **`ip address add  ` : add thêm một địa chỉ IP vào thiết bị mạng.**

  - Thêm một địa chỉ cho card eth1 với thời gian sử dụng địa chỉ là 100s và thời gian preferred là 50s:

  `ip a add 10.10.10.20/24 dev eth1 valid_lft 100 preferred_lft 50`

- **`ip address del  `: Xóa một địa chỉ trên thiết bị** 

  Ví dụ: 

  `ip a delete 10.10.10.20/24 dev eth1`

- **`ip a show`:	Show ra thông tin các thiết bị.**

  - Ví dụ show ra thông tin địa chỉ IP của các thiết bị đang ở trạng thái up:

  `ip a show up`

  -	Hoặc show ra thông tin các thiết bị có địa chỉ IP trong mạng 10.10.10.0/24

  `ip a show to 10.10.10.0/24`

-	**`ip a flush`: Giải phóng địa chỉ IP khỏi thiết bị theo điều kiện đưa ra**

  - Ví dụ: Giải phóng địa chỉ IP khỏi thiết bị eth1 với prefix là trong dải mạng 10.10.10.0/24:

  `ip address flush dev eth1 to 10.10.10.0/24`

<img src ="http://imgur.com/Vn2Z3df.jpg">

<a name ="4"></a>
# 4. Câu lệnh ip route

<a name = "4.1"></a>
## 4.1. Giới thiệu

\- Là câu lệnh quản lý các bảng định tuyến (routing tables).

\- Là một phần của **iproute2** cho việc quản lý IP, `ip route` cung cấp công cụ quản lý cho bất kì thao tác làm việc trong bảng định tuyến – routing table. Nó có khả năng **mô tả các đường định tuyến hoặc định tuyến trong cache – routing cache, thêm, xóa, chỉnh sửa các đường định tuyến**.

\- Một điều cần nhớ là khi sử dụng `ip route` ta có thể thao tác với **255 bảng định tuyến** bằng dòng lệnh, trong khi lệnh `route` chỉ thao tác được với **bảng main – main routing table (table 254)**. Lệnh `ip route` thao tác mặc định trong bảng main, nhưng cũng có thể dễ dàng thay đổi sang bảng khác dùng thông số `table` trong phần tùy chọn.

<a name = "4.2"></a>
## 4.2. Cấu trúc câu lệnh

```
ip [ ip-OPTIONS ] route  { COMMAND | help }

ip route get ADDRESS [ from ADDRESS iif STRING  ] [ oif STRING ] [ tos TOS ]

ip route { add | del | change | append | replace } ROUTE
```

Tham khảo thêm các thành phần trong câu lệnh `ip route` tại [manpage ip-route](http://manpages.ubuntu.com/manpages/xenial/en/man8/ip-route.8.html)

<a name = "4.3"></a>
## 4.3. Một số ví dụ phổ biển với `ip route`

- **`ip route show` : Biểu diễn bảng định tuyến**

  \- Biểu diễn bảng định tuyến: sử dụng `ip route show`, khi đó sẽ hiển thị bảng định tuyến main routing table. 

  \- Thêm tùy chọn `table TABLE_ID` để xem các thông tin định tuyến trong các bảng khác:

<img src = "http://imgur.com/Eie0jAJ.jpg">


- **`ip route add`: Thêm định tuyến vào bảng định tuyến**

  \- Thêm một đường định tuyến tĩnh: `ip route add 10.10.10.0/24 via 172.16.100.10` : Ta vừa thêm vào bảng định tuyến đường đi cho các gói tin có đích trong dải 10.10.10.0/24. Kiểm tra lệnh ping như sau:

<img src = "http://imgur.com/58tHTrB.jpg">

  Kết quả gói tin icmp unreachable trả về từ 172.16.100.10

  \- Thêm một định tuyến loại unreachable không cho phép các gói tin định tuyến đi tới địa chỉ 10.10.10.2 (đã có card eth1 địa chỉ 10.10.10.10)

<img src = "http://imgur.com/X1wfX6i.jpg">

  \- Add thêm một default gateway cho máy: `ip route add default via *ADDRESS*`

<img src = "http://imgur.com/j8dG5oZ.jpg">

- **`ip route del`: Xóa static route**

  \- Xóa đi định tuyến unreachable vừa tạo bên trên: 

<img src = "http://imgur.com/FutnXmp.jpg">

  \- Xóa đi default gateway vừa thêm:

<img src = "http://imgur.com/O6B4a0o.jpg">


- **`ip route change`: Thay đổi thông tin định tuyến**

  Ví dụ : thay đổi default gateway:

<img src = "http://imgur.com/hsSdXlX.jpg">


- **`ip route get`: Lấy thông tin định tuyến cho một địa chỉ đích đưa ra. (có thể thêm tùy chọn -s để biết thông tin định tuyến sử dụng trong cache)**

<img src = "http://imgur.com/9KybZDi.jpg">

- **`ip route flush`: Xóa thông tin trong bảng định tuyến**

<img src = "http://imgur.com/yUeugGO.jpg">


<a name = "5"></a>
# 5. Tham khảo

[1] ip manpage: http://manpages.ubuntu.com/manpages/xenial/en/man8/ip.8.html

[2] ip link manpage:http://manpages.ubuntu.com/manpages/xenial/en/man8/ip-link.8.html

[3] ip address manpage: http://manpages.ubuntu.com/manpages/xenial/en/man8/ip-address.8.html

[4] ip route : http://manpages.ubuntu.com/manpages/xenial/en/man8/ip-route.8.html



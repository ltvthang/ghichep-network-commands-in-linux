# ip command


# MỤC LỤC
- [1. Introduction ip command](#1)
- [2.ip link  command - network device configuration](#2)
- [3.ip address command - Protocol Address Management ](#3)
- [4.ip route - routing table management](#4)
- [THAM KHẢO](#thamkhao)


<a name="1"></a>
# 1. Introduction ip command
\- ip command có tác dụng show và thao tác với routing, devices, policy routing and tunnels .  
\- Cú pháp :  
```
ip [ <OPTIONS> ] <OBJECT> { <COMMAND> | help }
```
trong đó :  
- OBJECT := { link | addr | addrlabel | route | rule | neigh | ntable |tunnel | tuntap | maddr | mroute | mrule | monitor | xfrm | netns | l2tp | tcp_metrics }
- OPTIONS := { -V[ersion] | -s[tatistics] | -r[esolve] | -f[amily] { inet| inet6 | ipx | dnet | link } | -o[neline] }

Tham khảo : http://manpages.ubuntu.com/manpages/trusty/man8/ip.8.html  

\- Sau đây mình sẽ trình bày một số ip command hay dùng như `ip link`, `ip a`, `ip route` .  

<a name="2"></a>
# 2.ip link  command - network device configuration
## 2.1.Giới thiệu
\- ip link command để cấu hình network device .  
\- Cú pháp :  
```
ip [ <OPTIONS> ] link  { <COMMAND> | help }
```

\- Tham khảo trong : http://manpages.ubuntu.com/manpages/trusty/man8/ip-link.8.html  
\- Sau đây là một số command hay dùng của `ip link` như `ip link show` ,`ip link se` ,`ip link add` ,`ip link delete` .  

## 2.2.ip link show 
\- ip link show - display device attributes .  
\- Cú pháp :  
```
ip link show [dev <NAME>]
```

\- Example :  
```
ip link
ip link show
ip link show ens33
```

<img src="http://i.imgur.com/DYnCDNo.png" >

## 2.3.ip link set
\- `ip link set` - change device attributes .  
\- Cú pháp :  
```
ip link set dev <NAME> {up|down}
```

\- Example :  
```
ip link set ens33 up
```

## 2.4.ip link add
\- ip link add - add virtual link .  
\- Cú pháp :  
```
ip link add <NIC> type {TYPE}
```

TYPE := [ bridge | can | dummy | ifb | ipoib | macvlan | vcan | veth | vlan | vxlan | ip6tnl | ipip | sit | gre | gretap | ip6gre |ip6gretap ]

\- Example :  
```
root@ubuntu:/home/winterwind# ip link add br0 type bridge
root@ubuntu:/home/winterwind# brctl show
bridge name	bridge id		STP enabled	interfaces
br0		8000.000000000000	no			
virbr0	8000.000000000000	yes		
```

\- Note : Câu lệnh này sẽ add bridge – chính là linux bridge .  

## 2.5.ip link delete
\- ip link delete - delete virtual link .  
\- Cú pháp :  
```
ip link delete <NIC>
```

\- Example :  
```
ip link delete br0
```  


# 3.ip address command - Protocol Address Management 
## 3.1.Giới thiệu
\- ip-address command để quản lý address network device .  
\- Cú pháp :  
``` 
ip [ <OPTIONS> ] address  { <COMMAND> | help }
```

\- `ip address` <=> `ip addr` <=> `ip a` .  

\- Tham khảo : http://manpages.ubuntu.com/manpages/xenial/man8/ip-address.8.html  
\- Sau đây là một số `ip a` command hay dùng như : `ip a show` ,`ip a add` ,`ip a del` ,`ip a flush` .
## 3.2.ip a show
\- `ip a show` có tác dụng show network device address .  
\- Cú pháp :  
```
ip a show [dev <NIC>] [up]
```

\- Example :  
```
ip a show
ip a
ip a show dev ens33
ip a show up   #show những network device đang bật
```

<img src="http://i.imgur.com/avnLEmu.png" >

## 3.3.ip a {add|del}
\- ip address add - add new protocol address.  
ip address delete - delete protocol address .  
\- Cú pháp :  
```
ip a {add|del} <IP_address> dev <NIC>
```
\- Example :  
```
ip a add 172.16.69.200/24 dev ens33
```

<img src="http://i.imgur.com/ebD4osl.png" >

## 3.4. ip address flush 
\- ip address flush - flush protocol addresses .  
\- Example : Removes all addresses from device ens33 
```
ip addr flush dev ens33
```

<a name="4"></a>
# 4.ip route - routing table management
## 4.1.Giới thiệu
\- ip-route - routing table management .
\- Cú pháp :
```
ip [ <OPTIONS> ] route  { <COMMAND> | help }
```

\- Tham khảo : http://manpages.ubuntu.com/manpages/xenial/man8/ip-route.8.html  
\- Sau đây là một số `ip route` command hay dùng như : `ip route show` ,`ip route add` ,`ip route delete` .  

## 4.2.ip route show
\- `ip route show` : Displays the contents of the routing .  
\- Example :  
```
ip route show 
ip route
ip route list
```

<img src="http://i.imgur.com/2bnRLQL.png" >

## 4.3.ip route add|delete
\- `ip route add` :  add new route  
`ip route del` : delete route  
\- Syntax  
```
ip route { add | delete } <network_address|IP_address> via <IP_addrses> [dev <NIC_name>]
```

\- Example :  
- Add Static Route  
```
ip route add 192.168.1.104 via 172.16.69.100 dev ens33 # or ip route add 192.168.1.104 via 172.16.69.100
ip route add 192.168.1.0/24 via 172.16.69.100 dev ens33
```

**Note** : Nếu muốn “Add Persistence Static Routes” thì confg in file 1/etc/network/interfaces1 đối với OS **Ubuntu/Debian/Linux Mint** .  
Config với NIC như thường và thêm dòng :  
```
up <command>
```

Ví dụ :  
```
auto ens33
iface ens33 inet static
address 172.16.69.100/24
gateway 172.16.69.1
#########{Static Route}###########
up ip route add 10.10.10.0/24 via 172.16.69.1 dev ens33
```

> `up ip route add 10.10.10.0/24 via 172.16.69.1 dev ens33` : Những packet có “Destination IP address”  thuộc network address `10.10.10.0/24` thì phải đi qua 172.16.69.1 thông qua NIC ens33 .  

- Add defualt gateway
```
ip route add default via 172.16.69.1
```

- Remove Static Route
```
ip route del 192.168.1.104
```
- Remove default gateway
```
ip route del default
```

<a name="thamkhao"></a>
# THAM KHẢO
- ip command  :  
http://manpages.ubuntu.com/manpages/trusty/man8/ip.8.html  
http://www.tecmint.com/ip-command-examples/  
https://www.youtube.com/watch?v=wWyL6DdHYBc&t=31s  
  - ip link : http://manpages.ubuntu.com/manpages/trusty/man8/ip-link.8.html
  - ip address : http://manpages.ubuntu.com/manpages/xenial/man8/ip-address.8.html  
  - ip route : http://manpages.ubuntu.com/manpages/xenial/man8/ip-route.8.html  






















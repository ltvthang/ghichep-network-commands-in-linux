# net tool package and iproute2 package

# MỤC LỤC
- [1.net tool](#1)
- [2.iproute2](#2)
- [THAM KHẢO](#thamkhao)




<a name="1"></a>
# 1.net tool
\- Net tool là :  
- Collection of programs that form the base set of the NET-3 networking distribution for the Linux operating system. 
- This package includes `arp`(8), `hostname`(1), `ifconfig(8)`, `ipmaddr`, `iptunnel`, `mii-tool`(8), `nameif`(8), `netstat`(8), `plipconfig`(8), `rarp`(8), `route`(8) and `slattach`(8).

\- Net tool program là đã lỗi thời và được thay thế vởi `iproute2` program .  

|program|obsoleted by|
|-------|------------|
|arp|ip neigh|
|ifconfig|ip addr|
|ipmaddr|ip maddr|
|iptunnel|ip tunnel|
|route|ip route|
|nameif|ifrename|
|mii-tool|ethtool|

\- Có sẵn trong hầu hết các distribution ( thường viết tắt là distro ) của  Linux .  


<a name="2"></a>
# 2.iproute2
\- `iproute2` is a collection of userspace utilities for controlling and monitoring various aspects of networking in the Linux kernel, including **routing**, **network interfaces**, **tunnels**, **traffic control**, and **network-related device drivers**.  
\- `iproute2` is an open-source project released under the terms of version 2 of the GNU GPL license .  
\- `iproute2` collection contains the following command-line utilities: `ip`, `ss`, `bridge`, `rtacct`, `rtmon`, `tc`, `ctstat`, `lnstat`, `nstat`, `routef`, `routel`, `rtstat`, `tipc`, `arpd` and `devlink`.  
\- `iproute2` utilities communicate with the Linux kernel using the **netlink protocol**.  
\- `iproute2` thay thế `net tool` .  

<a name="thamkhao"></a>
# THAM KHẢO
https://wiki.linuxfoundation.org/networking/net-tools  
http://net-tools.sourceforge.net/  
https://en.wikipedia.org/wiki/Iproute2  
https://wiki.linuxfoundation.org/networking/iproute2  
	



















# ping command and fping command


# MỤC LỤC
- [1.ping command](#1)
  - [1.1.Giới thiệu](#1.1)
  - [1.2.Example](#1.2)
- [2.fping command](#2)
  - [2.1.Giới thiệu](#2.1)
  - [2.2.Install fping tool](#2.2)
  - [2.3.Example](#2.3)
- [THAM KHẢO](#thamkhao)


<a name="1"></a>
# 1.ping command
<a name="1.`"></a>
# 1.1.Giới thiệu
\- `ping`, `ping6` - send ICMP ECHO_REQUEST to network hosts .  
\- `ping` thường được sử dụng để kiểm tra có máy tính có mạng hay không ?  
\- Cú pháp :  
```
ping [option]
```

\- Tham khảo : http://manpages.ubuntu.com/manpages/xenial/man8/ping.8.html  

<a name="1.1"></a>
# 1.2.Example
\- VD1 : Ping without option  
```
ping google.com
```

<img src="http://i.imgur.com/xoEfygG.png" >  

\- VD2 : Increase or Decrease the Time Interval Between Packets use `–i` option  
- Increase Ping Time Interval  
Example: Wait for 5 seconds before sending the next packet.  
```
ping -i 5 google.com
```

- Decrease Ping Time Interval  
Example: Wait 0.1 seconds before sending the next packet.  
```
ping -i 0.1 8.8.8.8
```

\- VD3 : Check whether the local network interface is up and running  
- Ping localhost using zero (0)  
```
ping 0
```

- Ping localhost using name  
```
ping localhost
```

\- VD4 : Send N packets and stop use `-o` option
```
ping –c 3 google.com
```

<img src="http://i.imgur.com/ZQDExBa.png" >  

\- VD5 : Flood the network use `-f` option  
```
ping –f google.com
```

<img src="http://i.imgur.com/42XkLod.png" >  

Ta thấy , host đã gửi 264 packets trong vài giây .  
\- VD6 : Print Only Ping Command Summary Statistics use `-q` option  
```
ping -c 3 -q google.com
```

<img src="http://i.imgur.com/c1cHhJV.png" >  

\- VD7 : Change Ping Packet Size use `-s` option  
```
ping -s 100 google.com
```

<img src="http://i.imgur.com/cxFaJFG.png" >  

\- VD8 : Timeout use `-w` option  
Chỉ định thời gian thoát của ping commnad .  
```
ping –w 5 google.com
```

<img src="http://i.imgur.com/sFvBwEs.png" >  

>Note : Nếu sử dụng cả 2 `-w` và `-c` option thì cái nào đến trước sẽ chấm dứt ping command .

\- VD8 : Sử dụng `CTRL  + |` (Control key followed by pipe symbol) để show thống kê ở giữa , trong khi vẫn tiếp tục sending và receiving packet  

<img src="http://i.imgur.com/f2xmQcT.png" >  

\- VD9 : Specify path for ping to send the packet  
You can also specify through which path the ping should send the packet to destination.  
```
ping <hop1> <hop2> <hop3> .. <hopN> <destination>
```

>Note: If one of the hop in the path is not reachable then you will have failure in pinging.

\- VD10 : Record and print route of how ECHO_REQUEST sent and ECHO_REPLY received  
It records, and prints the network route through which the packet is sent and received. This is useful for network engineers who wish to know how the packet is sent and received.  
```
ping –R 8.8.8.8
```

<img src="http://i.imgur.com/KrGmDOx.png" >  

\- VD11 :Ping sử dụng network card chỉ định  
```
ping –I ens33 8.8.8.8
```

<img src="http://i.imgur.com/dqp7wAx.png" >  

<a name="2"></a>
# 2.fping command
<a name="2.1"></a>
## 2.1.Giới thiệu
\- `fping` command − send ICMP ECHO_REQUEST packets to network hosts .  
\- `fping` là command tương tự như `ping` nhưng có nhiều điểm hay hơn .  
\- Cú pháp :  
```
fping [ <options> ] [ <systems>... ]
```

\- Tham khảo : https://fping.org/fping.1.html  

<a name="2.2"></a>
## 2.2.Install fping tool
\- On Ubuntu Server 16.04  
```
sudo apt-get install fping
```

## 2.3.Example
### 1.Fping one IP Address
```
fping 8.8.8.8
```

<img src="http://i.imgur.com/MuhmldW.png" >  

### 2.Fping multiple IP Address
```
fping 8.8.4.4 8.8.8.8 google.com
```

<img src="http://i.imgur.com/eVaVVZF.png" >  

### 3. Fping Range of IP address
```
fping -s -g 192.168.1.1 192.168.1.5
#or fping –g 192.168.1.0/24
```

<img src="http://i.imgur.com/9yV9b6A.png" >  

### 4. Giới hạn số lần cố gắng ping đến một mục tiêu
```
fping –r 1 –g 192.168.1.0/24
```
>Note : “1’” là không tính lần ping đầu tiên .

### 5. Reads the List of Targets From a File
```
fping < fping.txt
#or
fping –f fping.txt
```

<img src="http://i.imgur.com/OU12e4w.png" >  

### 6.Ping sử dụng network card chỉ định
```
fping –I ens38 google.com
```

<img src="http://i.imgur.com/BwYpNs8.png" >  

### 7. Ping use IP_address chỉ định
```
fping -S 172.16.69.130 192.168.1.1
```

<img src="http://i.imgur.com/4ogSpyN.png" >  

<a name="thamkhao"></a>
# THAM KHẢO
- ping command : 
http://manpages.ubuntu.com/manpages/xenial/man8/ping.8.html  
http://www.thegeekstuff.com/2009/11/ping-tutorial-13-effective-ping-command-examples  
- fping command :
  - Mainpage :  
https://fping.org/  
https://fping.org/fping.1.html   
  - http://www.tecmint.com/install-fping-icmp-program-on-rhel-centos-6-5-4/  
https://www.youtube.com/watch?v=oh2foFGAp7o  












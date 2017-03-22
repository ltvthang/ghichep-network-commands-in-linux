# netstat command and ss command

# MỤC LỤC
- [1.netstat command](#1)
  - [1.1.Lý thuyết](#1.1)
  - [1.2.Thực hành](#1.2)
- [2.ss command](#2)
  - [2.1.Lý thuyết](#2.1)
  - [2.2.Thực hành](#2.2)
- [THỰC HÀNH](#thamkhao)




<a name="1"></a>
# 1.netstat command
<a name="1.1"></a>
## 1.1.Lý thuyết
\- netstat command : Print  network  connections,  routing  tables,  interface statistics, masquerade connections, and multicast memberships .  
\- Cú pháp :  
Tham khảo : http://manpages.ubuntu.com/manpages/xenial/man8/netstat.8.html

<a name="1.2"></a>
## 1.2.Thực hành
### 1.2.1. Port
\- Listing all ports (both TCP and UDP) using netstat `-a` option.  
```
netstat -a | more
```

<img src="http://i.imgur.com/Y4uZ2Sz.png" >

\- Show numerical address thay vì host , port or user names use `-n` option  
```
netstat -a -n | more   
# or 
netstat –an | more
```

<img src="http://i.imgur.com/zdgd4uV.png" >

-  Listing TCP Ports sockets use `-t` option
```
netstat –at
```

<img src="http://i.imgur.com/ZbJTvMr.png" >

- Listing UDP Ports use `-u` option
```
netstat -au
```
- Listing TCP and UDP Port is established
```
netstat -tu
```

<img src="http://i.imgur.com/gcs8VVh.png" >

- Listing all active listening ports connections with netstat `-l`
```
netstat -l
```

<img src="http://i.imgur.com/QUeXYLc.png" >

- Listing all active listening TCP ports by using  `netstat -lt`.

<img src="http://i.imgur.com/7ujn73k.png" >

- Listing all active listening UDP ports by using `netstat -lu`.
```
netstat -lu
```
- Listing all active UNIX listening ports using `netstat -lx`.

<img src="http://i.imgur.com/zFG2NZh.png" >

- Displaying Service name with PID  
Displaying service name with their PID number, using option `netstat -tp` will display “PID/Program Name”.  

<img src="http://i.imgur.com/Pv2BhRV.png" >

### 1.2.2. Displaying Kernel IP routing
\- Display Kernel IP routing table with netstat and route command.  
```
netstat -r
```

<img src="http://i.imgur.com/QlyaAl3.png" >

### 1.2.3. Showing Network Interface 
\- Showing network interface packet transactions including both transferring and receiving packets with MTU size.  
```
netstat -i
```

<img src="http://i.imgur.com/Rh4o26p.png" >

\- Showing Kernel interface table, similar to ifconfig command.  
```
netstat -ie
```

<img src="http://i.imgur.com/LsDJiGS.png" >

### 1.2.4. Displaying multicast IPv4 and IPv6 address
\- Displays multicast group membership information for both IPv4 and IPv6.  
```
netstat -g
```

<img src="http://i.imgur.com/3IbqxYY.png" >

### 1.2.5. Filter packet theo port
<img src="http://i.imgur.com/fyuKALE.png" >

<a name="2"></a>
# 2.ss command
<a name="2.1"></a>
## 2.1.Lý thuyết
\- ss command show information about socket . `ss` command có chức năng tương tự nhu `netstat` command nhưng có tốc độ nhanh và show nhiều thông tin hơn . ss command thuộc iproute2 package , trong khi đó netstat command thuộc net tool package - đã lỗi thời .  
\- Cú pháp :  
```
ss [ OPTIONS ] [ state <STATE-FILTER> ] [ <ADDRESS-FILTER> ]
```

\- Tham khảo :  
http://manpages.ubuntu.com/manpages/xenial/man8/ss.8.html  
https://www.apt-browse.org/browse/ubuntu/trusty/main/all/iproute2-doc/3.12.0-2/file/usr/share/doc/iproute2-doc/ss.html  

<a name="2.2"></a>
## 2.2.Thực hành
### 2.2.1. Listing listening , non-listening port or both listening and non-listening use -a -l option 
\- Listing both listening and non-listening sockets use `-a` option :
```
ss -a
```

<img src="http://i.imgur.com/dDNP1Uz.png" >  
<img src="http://i.imgur.com/jKsJ8el.png" >  

\- Listing all active listening ports connections use `-l` option :  
```
ss -l
```

<img src="http://i.imgur.com/Kk7AuEL.png" >

\- Listing non-listening ( thường là established ) sockets without option .  
```
ss
```

<img src="http://i.imgur.com/EJyFycO.png" >

\- Do not resolve hostname use `-n` option :  
```
ss -n
```

### 2.2.2.Listing TCP port , UDP port , unix port user `-t` , `-u` , `-x` 
\- Listing TCP port use `-t` option :  
```
ss -t
```

<img src="http://i.imgur.com/KvvB6YJ.png" >


\- Listing UDP port use `-u` option :  
```
ss -u
```

<img src="http://i.imgur.com/qY0UuSZ.png" >

\- Listing Unix Port use `-x` option :  
```
ss -x
```

<img src="http://i.imgur.com/NryMTgt.png" >

### 2.2.3.Listing process name and pid use -p option
```
ss -ltp
```

<img src="http://i.imgur.com/ikvrVgA.png" >

### 2.2.4.Show summary statistics use `-s` option
```
ss -s
```

<img src="http://i.imgur.com/Hp4ysrw.png" >


### 2.2.5.Show timer information use `-o` option
```
ss -o
```

<img src="http://i.imgur.com/a9boxMg.png" >

### 2.2.6.Filtering connections by state
\- Syntax :  
```
ss [option] [state <state-filter>]
```

\- VD : Show all TCP socket đang connected
```
ss -at state established
```

<img src="http://i.imgur.com/pUnZxsk.png" >


### 2.2.7.Filtering by addresses and ports\
\- Syntax:  
```
ss [option] [ADDRESS-FILTER]
```

\- VD : Display all established ssh connections.  
```
ss -o state established '( sport = :ssh or dport = :ssh )'
#or
ss -o state established sport = :ssh or dport = :ssh
```  

<img src="http://i.imgur.com/5HXEhPA.png" >

```
ss -o state established '( src :22 or dst  :22 )'
# or
ss -o state established '( src *:22 or dst *:22 )'
#or
ss -o state established src :22 or dst :22
```

<img src="http://i.imgur.com/wc65kuL.png" >

\- Một vài ví dụ khác :  
```
ss -tl '( src 172.16.69.0/24 and sport >= :15 )'
```
```
ss state established '( src 172.16.69.0/24 and sport >= :15 )'
```

<img src="http://i.imgur.com/HOOwSSo.png" >

<a name="thamkhao"></a>
# THAM KHẢO
- netstat command :
  - http://manpages.ubuntu.com/manpages/xenial/man8/netstat.8.html
  - http://www.tecmint.com/20-netstat-commands-for-linux-network-management/
- ss command :  
http://manpages.ubuntu.com/manpages/xenial/man8/ss.8.html  
https://www.apt-browse.org/browse/ubuntu/trusty/main/all/iproute2-doc/3.12.0-2/file/usr/share/doc/iproute2-doc/ss.html  
http://www.binarytides.com/linux-ss-command/  












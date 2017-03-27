# mtr command



# MỤC LỤC
- [1.Introduction](#1)
- [2. How mtr Works?](#2)
- [3.Install On Ubuntu server 16.04](#3)
- [4.Example](#4)
- [THAM KHẢO](#thamkhao)




<a name="1"></a>
# 1.Introduction
\- mtr combines the functionality of the traceroute and ping programs in a single network diagnostic tool.  

<a name="2"></a>
# 2. How mtr Works?
\- MTR works by sending ICMP packets by incrementally increasing the TTL value to find the route between the source and the given destination.  

<a name="3"></a>
# 3.Install On Ubuntu server 16.04
```
$ sudo apt-get install mtr
```

<a name="4"></a>
# 4.Example
\- VD1 : mtr `without` option  
```
mtr 8.8.8.8
```
\- VD2 : Configure the TTL value to start with use `-f` option  
```
mtr –f 2 8.8.8.8
```
\- VD3 : Configure the max hop use `-m` option  
```
mtr –m 5 8.8.8.8
```
\- VD4: Omit Reverse DNS using `--no-dns`  
MTR finds the hostname of each router/node by using Reverse DNS Lookup. If you want to avoid doing a reverse DNS lookup, use `–no-dns` option.  
```
mtr --no-dns 8.8.8.8
```
\- VD5 : Chỉ định số packek gửi cho mỗi hop using `-c` option  
```
mtr -c 3 8.8.8.8
```
\- VD6 : Execute mtr in Report Mode using `--report`  
In report mode, mtr will run for the number of cycles ( default 10 ), and then prints the statistics and exit. This mode will be useful for generating statstics about network quality.  
```
$ mtr --no-dns --report google.com

HOST: lakshmanan                  Loss%   Snt   Last   Avg  Best  Wrst StDev
  1.|-- 192.168.1.1                0.0%    10    2.5   3.0   2.4   4.2   0.6
  2.|-- 10.228.129.9               0.0%    10  235.0  74.4  34.0 235.0  67.9
  3.|-- 10.228.149.14              0.0%    10  154.8  65.5  38.7 154.8  34.8
  4.|-- 116.202.226.145            0.0%    10   60.9  66.9  48.2 102.4  15.4
  5.|-- 116.202.226.17             0.0%    10   54.1  65.1  36.0 194.5  46.8
  6.|-- 72.14.215.234              0.0%    10   44.5  78.8  39.2 252.7  64.5
  7.|-- 72.14.232.110              0.0%    10   55.7  66.4  39.1 179.8  41.8
  8.|-- 66.249.94.72               0.0%    10   68.9  90.3  68.9 133.6  18.6
  9.|-- 72.14.233.105              0.0%    10   68.8  76.3  68.8  92.2   7.3
 10.|-- 173.194.38.162             0.0%    10   88.7 107.3  72.2 293.1  65.8
 ```
Understand MTR Report  
- Lost% – Shows the % of packets loss at each hop.
- Snt – Shows the no:of:packets being sent.
- Last – Latency of the last packet being sent.
- Avg – Average latency of all packets.
- Best – Displays the best Round Trip Time for a packet to this host (shortest RTT).
- Wrst – Displays the worst Round Trip Time for a packet to this host (longest RTT).
- StDev – Provides the standard deviation of the latencies to each host.

\- VD7 : Use UDP datagrams instead of ICMP ECHO using `-u` option  
```
mtr -u 8.8.8.8
```


<a name="thamkhao"></a>
# THAM KHẢO
- Main page :  
https://bitwizard.nl/mtr/  
https://github.com/traviscross/mtr  
- http://manpages.ubuntu.com/manpages/xenial/man8/mtr.8.html  
http://www.thegeekstuff.com/2014/04/mtr-my-traceroute  










# Curl command


# MỤC LỤC
- [1.Lý thuyết](#1)
  - [a.Decription](#a)
  - [b.Syntax](#b)
  - [c.OPTIONS](#c)
- [2.Install on Ubuntu Server 16.04](#2)
- [3.Thực hành  ](#3)
- [THAM KHẢO](#thamkhao)





<a name="1"></a>
# 1.Lý thuyết
<a name="a"></a>
## a.Decription
`curl`  is  a tool to transfer data from or to a server, using one of the protocols (DICT, FILE, FTP, FTPS, GOPHER, HTTP, HTTPS,  IMAP, IMAPS,  LDAP,  LDAPS,  POP3, POP3S, RTMP, RTSP, SCP, SFTP, SMTP, SMTPS, TELNET and TFTP).   The  command  is  designed  to  work  without  user interaction.  

<a name="b"></a>
## b.Syntax
```
curl [options] [URL...]
```

\- Tham khảo : https://curl.haxx.se/docs/manpage.html  

<a name="c"></a>
## c.OPTIONS
Dưới đây cung cấp một số option phổ biến :  
### 1. `-o`, `--output` `<file>` : Write output to <file> instead of stdout
VD :  
```
curl -o aa example.com -o bb example.net
#or
curl example.com example.net -o aa -o bb
```

### 2. `-O`, `--remote-name`
Write output to a local file named like the remote file we get. (Only the file part of the remote file is used, the path is cut off.)  
VD :  
```
curl –O example.com
```  

### 3. `-L`, `--location`
(HTTP) If the server reports that the requested page has moved to a different location (indicated with a Location: header and a 3XX response code), this option will make curl redo the request on the new place  
VD :  
```
curl –L example.com
```

### 4. `-C`, `--continue-at` `<offset>`
\- Using curl `-C` option, you can continue a download which was stopped already for some reason. This will be helpful when you download large files, and the download got interrupted.  
\- Use "`-C -`" to tell curl to automatically find out where/how to resume the transfer. It then uses the given output/input files to figure that out.  
\- VD :  
```
curl –C - -O example.com
```

### 5. `--limit-rate` `<speed>`
\- Specify the maximum transfer rate you want curl to use - for both downloads and uploads.  
\- `speed` được đo bằng bytes/second (B) , KB,MG,GB .  
\- VD :  
```
curl --limit-rate 1000B example.com
```

### 6. `-z`, `--time-cond` `<time>`
\- (HTTP FTP) Request a file that has been modified later than the given time and date, or one that has been modified before that time.  
\- Start the date expression with a dash (-) to make it request for a document that is older than the given date/time, default is a document that is newer than the specified date/time.  
\- `<time>` <=> `dd-mm-yy` .  
-\ VD :  
- Command sau download yy.html được thay đổi sau ngày `21/12/2015`  
```
curl –z 21-Dec-15 example.com/yy.html 
```
- Command sau download yy.html được thay đổi trước ngày `21/12/2015`  
```
curl –z -21-Dec-15 example.com/yy.html 
```

### 7. `-u`, `--user` `<user:password>`
\- Specify the user name and password to use for server authentication.  
\- If you simply specify the user name, curl will prompt for a password.  
\- VD :  
```
curl –u winterwind example.com  
```
```
curl –u winterwind ftp://example.com 
```

### 8. `-T`, `--upload-file` `<file>`
\- This transfers the specified local file to the remote URL.  
\- VD :  
```
curl –T file1 ftp://example.com 
```
```
curl --upload-file "{file1,file2}" http://www.example.com
```
```
curl -T "img[1-1000].png" ftp://ftp.example.com/upload/
```

### 9. `-v`, `--verbose`
\- Makes curl verbose during the operation. Useful for debugging and seeing what's going on "under the hood". A line starting with '>' means "header data" sent by curl, '<' means "header data" received by curl that is hidden in normal cases, and a line starting with '*' means additional info provided by curl.  
\- VD :
``` 
curl -v http://example.com
```

### 10. `-x`, `--proxy` `[protocol://]host[:port]`
\- Use the specified proxy.  
\- VD :  
```
curl -x proxysever.test.com:3128 http://example.com
```

### 11.`--mail-from` `<address>`
(SMTP) Specify a single address that the given mail should get sent from.

### 12. `--mail-rcpt` `<address>`
\- (SMTP) Specify a single address, user name or mailing list name. Repeat this option several times to send to multiple recipients.  
\-When performing a mail transfer, the recipient should specify a valid email address to send the mail to.  
\-VD :
```
curl --mail-from winterwind@mail.com --mail-rcpt root@mail.com smtp://mailserver.com
```

\- Once the above command is entered, it will wait for the user to provide the data to mail. Once you’ve composed your message, type . (period) as the last line, which will send the email immediately.  
```
Subject: Testing
This is a test mail
.
```

<a name=".2"></a>
# 2.Install on Ubuntu Server 16.04
```
sudo apt-get install curl
```

<a name="3"></a>
# 3.Thực hành  
\- VD1 :  Command sau sẽ download content của URL và hiển thị ra STDOUT ( ví dụ như on your terminal )  
```
curl https://github.com/doxuanson/thuctap012017/tree/master/XuanSon
```

<img src="http://i.imgur.com/g8CJeaH.png" >  

Để save output trong file :  
```
curl https://github.com/doxuanson/thuctap012017/tree/master/XuanSon > XuanSon.md
```

<img src="http://i.imgur.com/JsZC68g.png" >  

\- VD2 : Save the cURL Output to a file  
```
curl -o test.md https://raw.githubusercontent.com/doxuanson/thuctap012017/master/XuanSon/Overview%20Linux/Linux%20distribution.md
```

<img src="http://i.imgur.com/n0UrmUU.png" >  

```
curl -O https://raw.githubusercontent.com/doxuanson/thuctap012017/master/XuanSon/Overview%20Linux/Linux%20distribution.md
```

<img src="http://i.imgur.com/jZ20C71.png" >  

\- VD3 : Fetch Multiple Files at a time  
```
curl -O https://raw.githubusercontent.com/doxuanson/thuctap012017/master/XuanSon/Overview%20Linux/Linux%20distribution.md -O https://raw.githubusercontent.com/doxuanson/thuctap012017/master/XuanSon/Overview%20Linux/Open%20source%20software%20and%20licence%20.md
```

<img src="http://i.imgur.com/MIDl5Ko.png" >  

\- VD4 : Follow HTTP Location Headers with `-L` option  
By default CURL doesn’t follow the HTTP Location headers. . Khi gõ “google.com” trong browser từ Việt Nam , nó sẽ tựu động chuyển hướng đến “google.com.vn” .

<img src="http://i.imgur.com/SBH43Lo.png" >  

Vì vậy ta cần thêm -L option để curl chuyển hướng :  
```
curl -L http://www.google.com 
```

<img src="http://i.imgur.com/Zhj3Pjo.png" >  

\- VD5 : More Information using Verbose and Trace Option  
```
curl -v google.com
```

<img src="http://i.imgur.com/MwTRtqt.png" >  

<a name="thamkhao"></a>
# THAM KHẢO
- Main page : https://curl.haxx.se/  
  - Docs : https://curl.haxx.se/docs/manpage.html  
- http://www.thegeekstuff.com/2012/04/curl-examples/?utm_source=feedburner  














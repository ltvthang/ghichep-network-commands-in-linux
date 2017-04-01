# Lệnh FPING 

# I. Giới thiệu về fping
## 1. Chương trình fping.

- Chức năng chính của fping cũng tương tự như ping để xác định một host từ xa có phản hồi hay không.
- fping có thể chỉ ra nhiều địa chỉ trên cùng một dòng lệnh hoặc dùng một danh sách chứa nhiều địa chỉ.
- Cú pháp: 
```sh
fping [options] [systems...]
```
	- options: danh sách các tùy chọn hỗ trợ trong fping.
	- systems: danh sách các địa chỉ cần kiểm tra.


## 2. Cài đặt fping
- Không như ping, fping không được cài đặt sẵn trong các distro của linux.

`sudo apt-get install - y fping`

## 3. Mã trạng thái
- 0: Tất cả các host cần ping đều có thể kết nối.
- 1: Có một vài địa chỉ không thể kết nối.
- 2: Có một vài địa chỉ không tìm thấy.
- 3: Khi tham số hệ thống không hợp lệ.
- 4: Lỗi hệ thống.

# II. Lab một số options trong fping

Một số tùy chọn của fping:
 ![Imgur](http://i.imgur.com/eSDxMia.png)

## 1. Thiết lập địa chỉ nguồn
Khi máy tính của chúng ta có nhiều giao tiếp mạng và nhiều địa chỉ IP cùng hoạt động, fping cho phép chúng ta chọn ra 1 giao tiếp mạng và 1 địa chỉ IP trong số các giao tiếp mạng và địa chỉ đang có để thực hiện ping từ giao tiếp mạng và địa chỉ đó. Địa chỉ ip phải là địa chỉ đã tồn tại trên máy tính. Tùy chọn **-S** là để chỉ ra địa chỉ nào dùng để ping chứ không phải là gán địa chỉ rồi ping. Tùy chọn **-I** để chọn một interface dùng để ping.

- `fping -S 10.10.10.3 google.com`
- `fping -I eth1 google.com`

## 2. Chế độ im lặng
Khi dùng chế độ im lặng, kết quả sẽ không được hiện thị lên màn hình. Chúng ta muốn biết được kết quả phải dựa vào mã trạng thái. `echo $?` để xem mã trạng thái.

![Imgur](http://i.imgur.com/SkLAFql.png)

## 3. Định dạng kết quả trả về.
- 1. hiện thị ra các host alive: `fping -a google.com` 
- 2. hiện thị ra các host unreachable: `fping -u google.com`
- 3. Chuyển đổi giữa IP và domain:

	- Khi fping dùng domain, kết quả trả về ip : `fping -A google.com`
	- ngược lại: `fping -d google.com`
	- ![Imgur](http://i.imgur.com/fHuBHpC.png)

- 4. Giới hạn gói tin gửi đi: `fping -c 2 google.com` gửi 2 gói tin.

## 4. Đọc danh sách địa chỉ từ tệp tin
`vi listAddress` tạo file chứa các địa chỉ ip và domain đề fping ![Imgur](http://i.imgur.com/DqDAcUi.png)

```sh
sudo fping -f listAddress
```

![Imgur](http://i.imgur.com/sU8b37e.png)
tùy chọn -f này phải thực hiện với quyền root.

## 5. Ping theo lớp mạng
- `-g addr/mask` : Tạo ra 1 danh sách mục tiêu từ 1 lớp mạng được cung cấp.
- `-g first_ip last_ip`: Tạo ra 1 danh sách mục tiêu từ 1 IP bắt đầu và 1 IP kết thúc.

![Imgur](http://i.imgur.com/3M13EKS.png)

---
# Trên đây là một số tùy chọn của fping


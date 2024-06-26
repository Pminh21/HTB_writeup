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
- Task 5: What is the password for the admin user on the website?: qwerty789
- Task 6: What option can be passed to sqlmap to try to get command execution via the sql injection?: --os-shell

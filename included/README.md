ip: 10.129.95.185
- tiến hành scan nmap:
- nmap -sV -T4 'ip'

 ![image](https://github.com/Pminh21/HTB_writeup/assets/169346714/62452d6b-535f-48e1-b6f5-1ebb8c0ea63f)
 
- Quét được apache chạy trên cổng 80.
-  Task 1: What service is running on the target machine over UDP? 
- sudo nmap  -Pn -sU --min-rate=4000 10.129.95.185 quét udp
![image](https://github.com/Pminh21/HTB_writeup/assets/169346714/bf086cc4-7732-4f8a-972e-3b3b5a619fe7)

- quét lỗi rồi đáp án có 4 chữ, chữ cuối là p, đề bài liên quan đến TFTP => giao thức là TFTP
- tiến hành truy cập vào trang web

 ![image](https://github.com/Pminh21/HTB_writeup/assets/169346714/270e3fef-0358-4f8e-9161-038e27317959)

- Url: http://10.129.95.185/?file=home.php nhìn trông giống lỗ hổng LFI
  + FIle Inclusion cho phép kẻ tấn công có thể xem các tệp trên máy chủ từ xa mà không cần nhìn thấy hoặc có thể thực thi các mã vào 1 mục tiêu bất kì trên trang web .
  + Điều này xảy ra là do trong code php web , lập trình viên đã sử dụng các lệnh include, require, include_once, require _ once , các lệnh này cho phép việc file hiện tại có thể gọi ra 1 file khác.
  + Dấu hiệu để nhận biết rằng trang web có thể tấn công file inclusion là đường link thường có dạng php?page=,hoặc php?file= ....
- Tiến hành khai thác thử: nhập ?file=/../../../../../etc/passwd
![image](https://github.com/Pminh21/HTB_writeup/assets/169346714/260315f0-b89f-4c45-b646-e348ce3a3e73)
- "tftp:x:110:113:tftp daemon,,,:/var/lib/tftpboot:/usr/sbin/nologin" 
- Task 3: What is the default system folder that TFTP uses to store files? /var/lib/tftpboot/ 
- Được luôn, ta thấy tên người dùng là mike.
- TFTP là giao thức chia sẻ file sinh ra từ năm 1970, cổ lỗ quá nên thiếu bảo mật, không yêu cầu xác thực người dùng.
- Không có chức năng lỉệt kê thư mục, đẩy 1 shell.php
- Lấy file có sẵn từ kali. Thay đổi ip của máy tấn công và đổi cổng thành 1234.
- ip mục tiêu đổi thành: 10.129.49.22

![image](https://github.com/Pminh21/HTB_writeup/assets/169346714/8d2609be-1701-401c-a077-341c9584f069)

- sau khi put lên, mở nc sử dụng cổng ta đã điền trong shell.php. Cổng 1337
![image](https://github.com/Pminh21/HTB_writeup/assets/169346714/83f9e74e-3cd3-4748-b9ff-0944e856e6e2)

- Cd vào thư mục var/www/html sử dụng lệnh ls -al để xem file ẩn.

![image](https://github.com/Pminh21/HTB_writeup/assets/169346714/2ad603ce-8a7a-4e12-81ef-317a12b31c53)

- Thấy được tên người dùng là mike như trước đó pass là: Sheffield19
- sử dụng lệnh su mike nhập mk: Sheffield19 để thay đổi user
- cd home, ls ta thấy có 1 file là user.txt tiến hành đọc file ra
- ![image](https://github.com/Pminh21/HTB_writeup/assets/169346714/11804040-01a7-4803-ac9b-132024402fce)

- Nhập lệnh ID

  ![image](https://github.com/Pminh21/HTB_writeup/assets/169346714/13115e20-c5af-418b-8f69-41d600abe853)

  - LXD là 1 trình quản lý contaniner cho hệ thống, người dùng ở nhóm lxd sẽ được quyền sudo mặc dù không được cấp mật khẩu root hay được cấp quyền sudo.
  - 




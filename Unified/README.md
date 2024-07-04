Ip mục tiêu là: 10.129.115.161
- Tiến hành quét nmap: nmap -sV -T4 10.129.115.161
  
![image](https://github.com/Pminh21/HTB_writeup/assets/169346714/6d2ae34b-15f4-448f-98e7-5764fc2a1989)

- có 4 cổng mở: 22,6789,8080,8443.
-  Task 1: Which are the first four open ports?: 22,6789,8080,8443
-  Tiếp tục sử dụng tham số -sC để tìm hiểu kĩ hơn về các dịch vụ đang chạy trên các cổng mở.

![image](https://github.com/Pminh21/HTB_writeup/assets/169346714/35a57b10-7c93-4439-ba31-3d628a75b82e)

-  Task 2: What is the title of the software that is running running on port 8443?: UniFi Network
-  Tiến hành truy cập trang web: https://10.129.115.161:8443

  ![image](https://github.com/Pminh21/HTB_writeup/assets/169346714/4b6fdee5-2b20-4281-a22a-4a2956d42940)

- Task 3: What is the version of the software that is running? 6.4.54
- Sớt google ra được CVE-2021-44228
- Task 4: What is the CVE for the identified vulnerability? CVE-2021-44228
- 

- ip: 10.129.229.142 
- scan nmap: nmap -sC -Pn -A 'ip' trong đó -A là quét hệ điều hành

  ![image](https://github.com/Pminh21/HTB_writeup/assets/169346714/5a6f6d94-7ec6-458b-b9b5-273598c8a0d1)

- Task 1: What version of Apache is running on the target's port 80?:  Apache/2.4.41


![image](https://github.com/Pminh21/HTB_writeup/assets/169346714/e0c867e6-b3f1-49e4-84d4-7b6f4765135d)

- Tiến hành nhập thử: admin:password được luôn
- Task 2: What username:password combination logs in successfully? admin:password 

![image](https://github.com/Pminh21/HTB_writeup/assets/169346714/817f7d9d-1add-42bd-bc94-72e4f63c6f19)

- Task 3: What is the word at the top of the page that accepts user input? order

-Task 4: What XML version is used on the target? 1.0

![image](https://github.com/Pminh21/HTB_writeup/assets/169346714/482bbfc1-3a12-4145-aac6-dd739ba0513e)

- Bật burp suite bắt request. Thì thấy ngay phiên bản là 1.0
- Task 5: What does the XXE / XEE attack acronym stand for?: XML External Entity
- (https://book.hacktricks.xyz/pentesting-web/xxe-xee-xml-external-entity)
- trong khi quét nmap ta nhận biết được hệ điều hành của mục tiêu là windowns 10
- Ta sẽ sử dụng <!DOCTYPE foo [ <!ENTITY ext SYSTEM "file:///etc/passwd" > ]> để lấy file rsa của daniel. Thư mục C:\Users\your_username\.ssh\.
- 
![image](https://github.com/user-attachments/assets/d41997f3-657d-41b8-9e86-2b5159921c65)

![image](https://github.com/user-attachments/assets/1cee386d-6bb9-49a8-9059-2d15b43da55b)

![image](https://github.com/user-attachments/assets/51234349-f114-45fc-8a8e-cc63c76a3672)

- Tạo 1 file id_rsa copy đoạn mã vào rồi tiến hành kết nối ssh.
![image](https://github.com/user-attachments/assets/e302ab0c-2a64-4727-a59d-fa17a35ca3e6)

![image](https://github.com/user-attachments/assets/9e90d411-276b-4cef-a292-66faddcfa0a3)

- Task 7 What is the file located in the Log-Management folder on the target? job.bat 
![image](https://github.com/user-attachments/assets/3b112583-9fde-473d-8c4b-db6ac7797043)
- Ta thấy chữ wevtutil. 
- Task 8: What executable is mentioned in the file mentioned before? 

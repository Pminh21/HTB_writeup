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
- 

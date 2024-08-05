- Ip: 10.10.10.138
- Scan xem có gì: nmap -T4 -sV 10.10.10.138
![Image 1](image/image1.png)

- nmap -T4 -sC  10.10.10.138
![Image 2](image/image2.png)

- Có cổng 20 và cổng 80 mở 
![Image 3](image/image3.png)

- Truy cập vào website, đọc thì thấy web được bảo vệ bởi công nghệ chống dos, không dùng dirsearch được. 
- Scan cổng 80: thử truy cập http://10.10.10.138/writeup.
![Image 4](image/image4.png)
- Có nội dung trong đấy 
- Inspect ra xem 
![Image 5](image/image5.png)
```
<meta name="Generator" content="CMS Made Simple - Copyright (C) 2004-2019. All rights reserved." />
```
- Phiên bản CMS made simple 2019 search xem có lỗ hổng nào không: CVE:2019-9053
<a href="https://www.exploit-db.com/exploits/46635">Exploit  CVE-2019-9053</a>
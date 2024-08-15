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
- Không chèn được script lên url, loại bỏ khả năng reflected xss, có 1 form nhập bình luận khả năng cao là stored xss.
- chèn thử 1 đoạn script và form 
 ![image 5](image/5.png)
 
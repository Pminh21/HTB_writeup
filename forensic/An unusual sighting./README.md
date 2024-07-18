
- Sử dụng netcat: nc  94.237.51.8 49257

![image](https://github.com/user-attachments/assets/dd0ef944-6c49-45d2-89c8-f82fe6b8100d)

- Giờ làm việc của Korp từ 9:00 đến 19:00
- Kiểm tra trong ssh_log và lịch sử bash. Xem có nhân vật nào đăng nhập ngoài thời gian này không.

![image](https://github.com/user-attachments/assets/0f653e2b-e7aa-4e50-b0d2-69d925d6fee1)

- What is the IP Address and Port of the SSH Server (IP:PORT) 100.107.36.130:2221
- What time is the first successful Login: 2024-02-13 11:29:50

![image](https://github.com/user-attachments/assets/8d6669e4-e228-4005-a753-4c211202a0fa)

- What is the time of the unusual Login: 2024-02-19 04:00:14 (thời gian ngoài giờ làm việc cyar Korp)
- What is the Fingerprint of the attacker's public key: OPkBSs6okUKraq8pYo4XwwBg55QSo210F09FCe1-yj4
- Chuyển sang tệp bash history:

  ![image](https://github.com/user-attachments/assets/4eaa1d4b-f6c9-4615-a624-a867cb87fd13)

- What is the first command the attacker executed after logging in > whoami
- What is the final command the attacker executed before logging out > ./setup
- Có vẻ như hacker đã tải lên server 1 file để thực thi. 


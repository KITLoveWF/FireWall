# FireWall
## Author: Mai Đức Kiên, Cao Khải Minh
## File lab 
[Lab08-FW.pdf](https://github.com/user-attachments/files/17437961/Lab08-FW.pdf)
### Setup Lab
For this lab, each student will need two (2) clients and one (1) server. We will use the following VMs:
1. Server (Guest): Ubuntu (SEEDUbuntu)
2. Client 1 (Guest): Ubuntu (with scapy installed)
3. Client 2 (Host): Windows 7 or 10
### Start processing the task
#### Check Ipaddress every computer
**1. We can test it with** *ipconfig* **command with win 11 machine and** *ifconfig* **command with ubuntu server and ubuntu client** <br><br>
**SEEDUbuntu**<br>

![Screenshot 2024-10-18 230602](https://github.com/user-attachments/assets/3ba3210b-f0f2-4565-884c-1dc3d36bd8b9) <br>
                               *SEED Ubuntu (192.168.64.133)* <br><br>

**Client Ubuntu**<br>
![Screenshot 2024-10-18 231033](https://github.com/user-attachments/assets/09c8164b-125f-457b-a1da-3348f2314b0a) <br>

  *Ubuntu Client(172.18.181.152)* <br><br>
**Client Win 11**<br>
![Screenshot 2024-10-18 231033](https://github.com/user-attachments/assets/d71c94c1-1055-46fe-b205-cb0de4b308d3) <br>
                                  *Win 11 (172.18.176.1)* <br><br>
**2. Ping with every machine**<br>

```bash
Ping 172.18.176.1
```


![Screenshot 2024-10-18 231352](https://github.com/user-attachments/assets/0dc2c509-a49c-4039-9fc5-abb9f0dea914)

```bash
Ping 192.168.64.133
```
![Screenshot 2024-10-18 231345](https://github.com/user-attachments/assets/d79089b7-8869-4a2f-8ef1-c4792b1004b4) 

```bash

Ping 172.18.176.1
```

![Screenshot 2024-10-18 232449](https://github.com/user-attachments/assets/d227b98b-2511-41a2-acb5-a2c670b2b90c)

**3.Checking FTP is working**
```bash
ftp <ip addr>
```
![Screenshot 2024-10-18 234425](https://github.com/user-attachments/assets/589aee5c-6d3a-46c2-ae52-38cf5c804ff5)





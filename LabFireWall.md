# FireWall
## Author: Mai Đức Kiên, Cao Khải Minh
## File lab 
[Lab08-FW.pdf](https://github.com/user-attachments/files/17437961/Lab08-FW.pdf)
### Setup Lab
For this lab, each student will need two (2) clients and one (1) server. We will use the following VMs:
1. Server (Guest): Ubuntu (SEEDUbuntu)
2. Client 1 (Guest): Ubuntu (with scapy installed)
3. Client 2 (Host): Windows 7 or 10

#### Check Ipaddress every computer
**1. We can test it with** *ipconfig* **command with win 11 machine and** *ifconfig* **command with ubuntu server and ubuntu client** <br><br>
### SEEDUbuntu (192.168.64.133) <br>

![Screenshot 2024-10-18 230602](https://github.com/user-attachments/assets/3ba3210b-f0f2-4565-884c-1dc3d36bd8b9) <br>
                             

### Client Ubuntu(192.168.64.130)** 
<br>
![image](https://github.com/user-attachments/assets/06a1311e-86b0-4fe4-99d6-58003e82d95d)
<br>

 
### Client Win 11(192.168.64.1)**
<br>
![image](https://github.com/user-attachments/assets/989e4925-4973-4377-a4b7-fdf34b678efc)
 <br>
**2. Ping with every machine**<br>
### SEEDUbuntu
```
Ping 192.168.64.130
```

![image](https://github.com/user-attachments/assets/64fc591e-a63a-44f8-920c-5cc0f76e7ad6)


### Win 11
```
Ping 192.168.64.133
```
![image](https://github.com/user-attachments/assets/01e54d9b-4098-48a4-922c-e89cb94c08a6)
 
### Ubuntu Client 
```

Ping 192.168.64.133
```
![image](https://github.com/user-attachments/assets/12435214-79a3-4f65-a633-1fcbf032618f)


**3.Checking FTP is working**
```bash
ftp <ip addr>
```
### Ubuntu Client
![image](https://github.com/user-attachments/assets/c62b8c77-860f-4b3c-abc0-8ce085a1f08c)
### SEEDUbuntu
![image](https://github.com/user-attachments/assets/7eff609c-d27f-4212-a781-e11d0bbd1540)



**4.Checking SSH service using PuTTY tool**

![Screenshot 2024-10-18 234814](https://github.com/user-attachments/assets/a4b83b2a-46a2-43b7-ad4d-06d217a20000)

![Screenshot 2024-10-18 234821](https://github.com/user-attachments/assets/2dcfb66e-28c7-4eb1-875d-b090594011dd)

**5.Rules Table**

```bash
sudo iptables -L
```

![Screenshot 2024-10-18 234729](https://github.com/user-attachments/assets/71730c2f-374a-47d1-b1ca-0ecafc6f33bd)


### Start processing the task <br>
**1.Change the default policy to DROP all access to Ubuntu server**  <br>
```bash
sudo iptables -P INPUT DROP
sudo iptables -P FORWARD DROP
sudo iptables -P OUTPUT DROP
```
![Screenshot 2024-10-19 210339](https://github.com/user-attachments/assets/115f2f0b-eedf-4e82-9cea-e9ea384e320b)

Check the result from either client machines (cannot ping, web access, ftp connect …)

*1.1.ClientUbuntu ping SeedUbuntu*
```
ping 192.168.64.133
```

![image](https://github.com/user-attachments/assets/e22de540-d85d-4db3-825f-1dda04b94834)


*1.2.Win 11 ping SeedUbuntu*
```
ping 192.168.64.133
```

![Screenshot 2024-10-19 210513](https://github.com/user-attachments/assets/878e8325-5106-4f7b-9731-d5577b23a439)

*1.3.ClientUbuntu ping by ftp SeedUbuntu*

```
ftp 192.168.64.133
```
![image](https://github.com/user-attachments/assets/1d6bd37c-e949-48b8-8b5c-7b1ed3e559e0)


*1.4.Win 11 ping by ftp SeedUbuntu*

```
ftp 192.168.64.133
```
![Screenshot 2024-10-19 211203](https://github.com/user-attachments/assets/79516f98-42fe-4a30-8293-8846ae59445c)

**2.Enable web and ftp access only for both clients**

```bash
sudo iptables -P INPUT DROP
sudo iptables -P FORWARD DROP
sudo iptables -P OUTPUT ACCEPT
```
![Screenshot 2024-10-19 234255](https://github.com/user-attachments/assets/21d018ef-9743-4062-bc02-9997233f40e2)

![Screenshot 2024-10-19 234308](https://github.com/user-attachments/assets/c2c99f91-f278-4821-91c6-a398def129a3)




Allow established connection

```bash
iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
```

Allow Win11 to access web port 80 (HTTP) and ftp service port 21

With ftp:
```bash
iptables -A INPUT -p tcp --dport 21 -j ACCEPT
iptables -A INPUT -p tcp --dport 30000:31000 -j ACCEPT
```

With web service:
```bash
iptables -A INPUT -p tcp --dport 80 -j ACCEPT
```



Check the rules table we can see that Win11 now have access to Web and ftp service


![Screenshot 2024-10-19 212403](https://github.com/user-attachments/assets/8c0a5a24-6317-444b-9a98-92d10f0471b3)


![Screenshot 2024-10-19 234600](https://github.com/user-attachments/assets/f22534d9-e5c0-4fec-a0cf-404f6bbb925f)












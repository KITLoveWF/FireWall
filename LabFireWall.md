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

![Screenshot 2024-10-19 210452](https://github.com/user-attachments/assets/93774b38-f029-4e9b-ab23-e19d35c6c4eb)

*1.2.Win 11 ping SeedUbuntu*

![Screenshot 2024-10-19 210513](https://github.com/user-attachments/assets/878e8325-5106-4f7b-9731-d5577b23a439)

*1.3.ClientUbuntu ping by ftp SeedUbuntu*

```bash
ftp 192.168.64.133
```
![Screenshot 2024-10-19 211158](https://github.com/user-attachments/assets/09c00cf9-f4e0-4188-8daa-acab8d0ed778)

*1.4.Win 11 ping by ftp SeedUbuntu*

```bash
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












# Jarkom-Modul-3-IUP6-2021
**Mukhoram Dimasputra Bagawan - 05111942000006**

**Fitriana Zahirah Tsabit - 05111942000011**

**Muhammad Rafi Hayla Arifa - 05111942000014**

### **Number 1**
First step is to make the topology <br>
![Screen Shot 2021-11-13 at 17 12 34](https://user-images.githubusercontent.com/74056954/141614822-5b3169db-c2ff-40e7-b874-a1dfe20a15df.png)

EniesLobby as DNS 
Server, Jipangu as DHCP Server, Water7 as Proxy Server <br>
EniesLobby use `bind9` <br>
Jipangu use `isc-dhcp-server` <br>
Water7 use `squid` <br>
Then, we can install one by one requirement on node <br>
```
# EniesLobby
apt-get update
apt-get install bind9 -y
```

```
# Jipangu
apt-get update
apt-get install isc-dhcp-server -y

cp -r shift3/default /etc/
cp -r shift3/dhcp /etc/

service isc-dhcp-server start
```

```
# Water7
apt-get update
apt-get install squid -y
```

and for Jipangu, we change config interfaces in `isc-dhcp-server` to `INTERFACES="eth0"`
<br>


### **Number 2**
Foosha as DHCP Relay we use `isc-dhcp-relay` then, we install on node <br>
```
apt-get update
apt-get install isc-dhcp-relay -y

cp -r shift3/default /etc/
cp -r shift3/network /etc/

service isc-dhcp-relay start
```
next, change config in relay `/etc/default/isc-dhcp-relay` with interfaces to the eth where want to relay. Server direct to Jipangu as Relay and Interfaces which is switch 1 2 3 <br>

```
SERVERS="192.122.2.4"
INTERFACES="eth1 eth2 eth3"
OPTIONS=""
```
![Screen Shot 2021-11-13 at 17 17 05](https://user-images.githubusercontent.com/74056954/141614942-016c5ddb-53d0-47a6-9b96-42b0c45f7468.png)

### **Number 3**
First, edit the network config Alabasta, Loguetown, Skypie, Tottoland to <br>
```
auto eth0
iface eth0 inet dhcp
```

Luffy and Zoro compiled the map. All existing clients MUST use the IP configuration from the DHCP Server. Clients passing through Switch1 get IP ranges from [IP prefix].1.20 - [IP prefix].1.99 and [IP prefix].1.150 - [IP prefix].1.169 <br>
![Screen Shot 2021-11-13 at 17 14 40](https://user-images.githubusercontent.com/74056954/141614890-c59c1d54-f4c5-40ed-80f2-c122096fa2bc.png)

### **Number 4**
Clients passing through Switch3 get IP ranges from [IP prefix].3.30 - [IP prefix].3.5 <br>
![Screen Shot 2021-11-13 at 17 16 19](https://user-images.githubusercontent.com/74056954/141614922-9422c6f6-b724-4e37-994c-f53ef7f27d25.png)

### **Number 5**
The client gets DNS from EniesLobby and the client can connect to the internet through the DNS. <br>
![Screen Shot 2021-11-13 at 17 18 23](https://user-images.githubusercontent.com/74056954/141614975-d370cadb-acab-4988-9ff3-7f192380024a.png)

### **Number 6**
The length of time the DHCP server lends an IP address to the client via Switch1 is 6 minutes, while the client via Switch3 is 12 minutes. With a maximum time allocated for borrowing an IP address for 120 minutes. <br>
![Screen Shot 2021-11-13 at 17 18 23](https://user-images.githubusercontent.com/74056954/141614975-d370cadb-acab-4988-9ff3-7f192380024a.png)

### **Number 7**
Luffy and Zoro plan to use Skypie as a server for buying and selling ships they own with a fixed IP address with IP [IP prefix].3.69. <br>
<img width="585" alt="141455958-bec8be39-23f7-418b-9c1f-1145a6768fa5" src="https://user-images.githubusercontent.com/74056954/141615014-df3131cd-77cd-4011-b7ea-7218357890fe.png">

<img width="415" alt="141455994-2b343b44-feba-4ac2-80a9-21dd80170072" src="https://user-images.githubusercontent.com/74056954/141615021-ea12a71a-5621-446d-9920-6723bf36679e.png">


### **Number 8**
Loguetown is used as a proxy client so that buying and selling transactions can be guaranteed security, as well as to prevent leakage of transaction data.

In Loguetown, the proxy must be accessible under the namejualbelikapal.yyy.com with the port used is 5000 <br>

### **Number 9**
To make buying and selling transactions more secure and there are two website users, proxy user authentication is installed with MD5 encryption with two usernames, namely luffybelikapalyyy with password luffy_yyy and zorobelikapalyyy with password zoro_ <br>

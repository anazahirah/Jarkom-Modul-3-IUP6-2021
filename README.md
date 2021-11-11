# Jarkom-Modul-3-IUP6-2021
### **Number 1**
First step is to make the topology <br>

EniesLobby as DNS Server, Jipangu as DHCP Server, Water7 as Proxy Server <br>
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


### **Number 3**
First, edit the network config Alabasta, Loguetown, Skypie, Tottoland to <br>
```
auto eth0
iface eth0 inet dhcp
```

Luffy and Zoro compiled the map. All existing clients MUST use the IP configuration from the DHCP Server. Clients passing through Switch1 get IP ranges from [IP prefix].1.20 - [IP prefix].1.99 and [IP prefix].1.150 - [IP prefix].1.169 <br>

### **Number 4**
Clients passing through Switch3 get IP ranges from [IP prefix].3.30 - [IP prefix].3.5 <br>

### **Number 5**
The client gets DNS from EniesLobby and the client can connect to the internet through the DNS. <br>

### **Number 6**
The length of time the DHCP server lends an IP address to the client via Switch1 is 6 minutes, while the client via Switch3 is 12 minutes. With a maximum time allocated for borrowing an IP address for 120 minutes. <br>

### **Number 7**
Luffy and Zoro plan to use Skypie as a server for buying and selling ships they own with a fixed IP address with IP [IP prefix].3.69. <br>

### **Number 8**
Loguetown is used as a proxy client so that buying and selling transactions can be guaranteed security, as well as to prevent leakage of transaction data.

In Loguetown, the proxy must be accessible under the namejualbelikapal.yyy.com with the port used is 5000 <br>

### **Number 9**
To make buying and selling transactions more secure and there are two website users, proxy user authentication is installed with MD5 encryption with two usernames, namely luffybelikapalyyy with password luffy_yyy and zorobelikapalyyy with password zoro_ <br>

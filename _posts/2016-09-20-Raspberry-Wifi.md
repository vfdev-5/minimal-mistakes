---
title: "Helper with wifi configuration on Raspberry"
categories:
  - robotics
tags:
  - ubuntu
  - raspberry
  - wifi
  - NetworkManager
---

### Configure using NetworkManager
Show available wifi:
```
nmcli dev wifi
```
Connect to a wifi
```
sudo nmcli dev wifi con "WifiSSID" password "mypassword" name "Name of Connection"
```
Edit connection :
```
sudo nmcli c edit "myconnection"
> set ipv4.method manual
> set ipv4.addr 192.168.43.5/24 192.168.43.7/24 192.168.43.55/24
> set ipv4.gateway 192.168.43.1
> set connection.autoconnect yes
> save persistent
> quit
```

### Setup static ip in terminal NOT using NetworkManager
Append to the file
```
sudo nano /etc/network/interface
>> auto wlan0
>> iface wlan0 inet static
>> address 192.168.43.5
>> netmask 255.255.255.0
>> gateway 192.168.43.1
>> wpa-ssid myconnection
>> wpa-psk <HEX_CODE>
```

### Links : 
- [Static ip WIFI](http://www.sudo-juice.com/how-to-a-set-static-ip-in-ubuntu/)
- [How to set up static IP address and why](http://askubuntu.com/questions/432506/when-are-network-broadcast-and-gateway-required-for-configuring-a-network-inter#432876)
- [Ubuntu NetworkManager](https://help.ubuntu.com/community/NetworkManager) and [nmcli man](http://manpages.ubuntu.com/manpages/wily/man1/nmcli.1.html)
- [Good network explaination in article](https://help.ubuntu.com/community/NetworkConfigurationCommandLine/Automatic)

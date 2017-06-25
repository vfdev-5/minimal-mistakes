---
title: "Helper with ROS, ssh, card dump on Raspberry"
categories:
  - robotics
tags:
  - ubuntu
  - raspberry
  - ROS
---

### Dump sd card
```
sudo ddrescue /dev/mmcblk0 saveRaspi2trustyandROSlast.img -S --size=14080M
sudo ddrescue saveRaspi2trustyandROSlast.img /dev/mmcblk0 -f
```

### Install ROS
```
sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
sudo apt-key adv --keyserver hkp://ha.pool.sks-keyservers.net:80 --recv-key 0xB01FA116
sudo apt-get update
sudo apt-get install ros-kinetic-ros-base
sudo rosdep init
rosdep update
echo "source /opt/ros/kinetic/setup.bash" >> ~/.bashrc
```

### SSH server
Install ssh server:
```
sudo apt install openssh-server
sudo cp /etc/ssh/sshd_config /etc/ssh/sshd_config.original
```
Configure:
sudo nano /etc/ssh/sshd_config
Add :
```
PubkeyAuthentication yes
```
and finally restart service:
```
sudo systemctl restart sshd.service
```
For info [here](https://help.ubuntu.com/lts/serverguide/openssh-server.html)

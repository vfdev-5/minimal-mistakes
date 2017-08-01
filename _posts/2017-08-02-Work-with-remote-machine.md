---
title: "How it could look like to work with remote machine"
categories:
  - remote-machine
tags:
  - Ubuntu 16.04
  - MacOSX
  - sshfs
  - Jupyter Notebook
---

This post gathers my notes on how to simplify developement work on remote machine. 
There is a bunch of various methods on this, I choose one the simpliest for me: `sshfs`.

My context is the following:
```

[Laptop]<--- ssh --->[Remote Machine]
Mac OSX               Ubuntu 16.04
```
I want to store files at the remote machine and edit them with *PyCharm*, *Jupyter Notebook*, etc.

### Primitive configuration: `~/.ssh/config`

The very simpliest setup to connect faster to the remote machine with `ssh` is to configure a `~/.ssh/config` file. For example:
```
Host XXXXX  # A machine name, e.g. supermachine
    HostName XX.XX.XX.XX  # IP   
    Port XXXXX # SSH Port, e.g. 22
    User XXXXX # User name, e.g. ubuntu
    IdentityFile ~/.ssh/id_rsa
    LocalForward 8888 0.0.0.0:8888  # Port forwarding for jupyter
```
Once connected to the remote machine, we can use `nano`, `vim` to create/edit files. Or launch *Jupyter Notebook* from remote machine:
```
jupyter notebook --port=8888 --ip=0.0.0.0 --no-browser
```
and open a browser on the laptop with the URL: `0.0.0.0:8888/tree`

Why not...

### Mount remote file system with `sshfs`

Another way to expose the filesystem of the remote machine in your laptop is with `sshfs`. 
On Mac OSX one can simply use `brew` to install it:
```
brew install sshfs
```
Then mount remote filesystem with an example command (if you have already configured `~/.ssh/config` file):
```
sshfs supermachine:/home/ubuntu/ /Users/USER/supermachine/ 
```
Once this is done, I use *PyCharm* to create/edit files directly on the remote machine. 

To run a script on the remote machine, I still need to connect with `ssh` on the machine and run manually the script.

Still, why not ...








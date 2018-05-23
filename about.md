---
layout: page
title: Manual Installation
permalink: /Documentation/
---

#### Requirements:
    - Ubuntu Server 16.04.2
    - linux kernel 4.4.0-75
    - dbgsym
    - make
    - g++
    - python
    - systemtap - 3.1
    

###### Download Ubuntu Server 16.04.2: 

Download Ubuntu Server 16.04.2 [download link](http://old-releases.ubuntu.com/releases/16.04.2/ubuntu-16.04.2-server-amd64.iso)

###### Installing Linux Headers: 

```shell
apt-get install linux-image-4.4.0-75-generic
apt-get install fdutils linux-source-4.4.0 linux-headers-4.4.0-75-generic
```

##### Installing dgbsym:

```shell
echo "deb http://ddebs.ubuntu.com $(lsb_release -cs) main restricted universe multiverse
deb http://ddebs.ubuntu.com $(lsb_release -cs)-updates main restricted universe multiverse
deb http://ddebs.ubuntu.com $(lsb_release -cs)-proposed main restricted universe multiverse" | \
sudo tee -a /etc/apt/sources.list.d/ddebs.list

sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 428D7C01 C8CAB6595FDFF622

sudo apt-get update

sudo apt-get install linux-image-4.4.0-75-generic-dbgsym

```
##### Installing make, g++ and python:
```shell
sudo apt-get install make
sudo apt-get install g++
sudo apt-get install python
```

##### Installing systemtap:
Download systemtap 3.1 [[download file]](https://sourceware.org/systemtap/ftp/releases/systemtap-3.1.tar.gz)

```shell
wget https://sourceware.org/systemtap/ftp/releases/systemtap-3.1.tar.gz
tar -xvzf systemtap-3.1.tar.gz

cd systemtap-3.1
sudo apt-get install gettext
apt-get install libdw-dev

./configure
sudo su
make
make install

rm -rf /root/.systemstap/*.*
reboot
```

#### Installation:

In order to test the whole installation package:

```shell
 stap  -e  ’probe  begin   printf(”Hello,  World!”)’;
 exit() 
```

##### Downloading IntP:
```shell
function gdrive_download () {
 CONFIRM=$(wget --quiet --save-cookies /tmp/cookies.txt --keep-session-cookies --no-check-certificate "https://docs.google.com/uc?export=download&id=$1" -O- | sed -rn 's/.*confirm=([0-9A-Za-z_]+).*/\1\n/p')
 wget --load-cookies /tmp/cookies.txt "https://docs.google.com/uc?export=download&confirm=$CONFIRM&id=$1" -O $2
 rm -rf /tmp/cookies.txt
}
```

```shell
gdrive_download 0B4kSFaKe-Rt9dnY2LThVWEZ1dEdjNTQ3UFdTclZmYUtQRFBB intp.stp
```

### Execution
It is important to note that you must run the command stap as root.
```shell
stap --suppress-handler-errors -g son0.stp ApplicationName
```


### Outputs
Receiving Return:

```shell
$ watch -n2 -d cat /proc/systemtap/stap_*/intestbench
```

IntP returns the interference metrics for CPU, disk, memory, network, and cache. More specifically, it returns the following metrics:

* netp - percentage of physical network
* nets - percentage of network queue interference.
* blk - percentage of disk interference.
* mbw - percentage of memory bus interference.
* llcmr - percentage of cache miss.
* llocc - percentage of cache interference.
* cpu - percentage of cpu interference.

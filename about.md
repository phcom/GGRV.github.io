---
layout: page
title: Manual Installation
permalink: /Documentation/
---

#### Requirements:

    - g++
    - systemtap - 3.1
    - dbgsym
    - Linux Kernel 4.4.0-75

Install Systemtap 3.1
Download systemtap 3.1 [donwload page](https://sourceware.org/systemtap/ftp/releases/systemtap-3.1.tar.gz)

```shel
wget https://sourceware.org/systemtap/ftp/releases/systemtap-3.1.tar.gz
tar systemtap-3.1.tar.gz
```
On systemtap folder use comando make

On the folder /tmp/systemtap-3.1 make install


Install Linux Kernel on Ubuntu Server 16.04-2: [view download page](https://packages.ubuntu.com/xenial/linux-image-4.4.0-75-generic)


```shell
sudo apt-get install linux-image-4.4.0-75-generic
wget http://mirrors.kernel.org/ubuntu/pool/main/l/linux-lts-xenial/linux-image-4.4.0-75-generic_4.4.0-75.96~14.04.1_amd64.deb

sudo dpkg -i linux-image-4.4.0-75-generic-dbgsym4.4.0-75.96amd64.ddeb
```

Intall dgbsym

```shel
echo "deb http://ddebs.ubuntu.com $(lsb_release -cs) main restricted universe multiverse
deb http://ddebs.ubuntu.com $(lsb_release -cs)-updates main restricted universe multiverse
deb http://ddebs.ubuntu.com $(lsb_release -cs)-proposed main restricted universe multiverse" | \
sudo tee -a /etc/apt/sources.list.d/ddebs.list

sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 428D7C01 C8CAB6595FDFF622

sudo apt-get update

sudo apt-get install linux-image-4.4.0-75-generic-dbgsym
```


#### Installation:

```shell
apt-get install fdutils linux-source-4.4.0 linux-headers-4.4.0-75-generic
```

In order to test the whole installation package:

```shell
 stap  -e  ’probe  begin   printf(”Hello,  World!”);
 exit() 
```

### Execution
It is important to note that you must run the command stap as root.
```shell
stap –suppress-handler-errors -g son0.stp ApplicationName
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
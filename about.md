---
layout: page
title: Manual Installation
permalink: /Documentation/
---

#### Requirements:
    - Linux Kernel 4.4.0-75
    - dbgsym
    - make
    - g++
    - python
    - systemtap - 3.1
    

###### Installing Linux Headers: 

```shell
apt-get install linux-image-4.4.0-75-generic
apt-get install fdutils linux-source-4.4.0 linux-headers-4.4.0-75-generic
```

##### Installing dgbsym

```shell
echo "deb http://ddebs.ubuntu.com $(lsb_release -cs) main restricted universe multiverse
deb http://ddebs.ubuntu.com $(lsb_release -cs)-updates main restricted universe multiverse
deb http://ddebs.ubuntu.com $(lsb_release -cs)-proposed main restricted universe multiverse" | \
sudo tee -a /etc/apt/sources.list.d/ddebs.list

sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 428D7C01 C8CAB6595FDFF622

sudo apt-get update

sudo apt-get install linux-image-4.4.0-75-generic-dbgsym

```
##### Installing make and g++:
```shell
sudo apt-get install make
sudo apt-get install g++
```

##### Installing systemtap:
Download systemtap 3.1 [download page](https://sourceware.org/systemtap/ftp/releases/systemtap-3.1.tar.gz)

```shell
wget https://sourceware.org/systemtap/ftp/releases/systemtap-3.1.tar.gz
tar xvzf systemtap-3.1.tar.gz

cd systemtap-3.1
sudo apt-get install gettext
apt-get install libdw-dev

./configure
make
make install
```

#### Installation:

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
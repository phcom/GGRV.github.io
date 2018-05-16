---
layout: page
permalink: /Documentation/
---

## Manual Installation

#### Requirements:

    - gcc
    - systemtap
    - systemtap-runtime
    - Linux Kernel 4.4.0-75 

Install Linux Kernel on Ubuntu Server 16.04-2: [view download page](https://packages.ubuntu.com/xenial/linux-image-4.4.0-75-generic)

```shell
wget http://ddebs.ubuntu.com/pool/main/l/linux/linux-image-4.4.0-75-generic-dbgsym4.4.0−75.96amd64.ddeb

sudo dpkg -i linux-image-4.4.0-75-generic-dbgsym4.4.0-75.96amd64.ddeb
```

#### Installation:

```shell
sudo apt-get install linux-headers-$(uname -r)
sudo apt-get install kernel-devel-$(uname -r)
sudo apt-get install kernel-debuginfo-$(uname -r)

```

In order to test the whole installation package:

```shell
 stap  -e  ’probe  begin   printf(”Hello,  World!”);
 exit() 
```

### Execution

```shell
sudo apt-get install kernel-debuginfo-common-$(uname -m)-$(uname -r)

stap –suppress-handler-errors -g son0.stp ApplicationName
```

### Contact

[Prof. Dr. César Augusto Fonticielha De Rose](mailto:cesar.derose@pucrs.br)  
[Prof. Dr. Miguel Gomes Xavier](mailto:miguel.xavier@pucrs.br)
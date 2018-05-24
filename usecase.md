---
layout: page
title: Installing stress-ng through apt-get repository
permalink: /Usecase/
---

```shell
apt-get install stress-ng
```
## Stress-ng tutorial using IntP:
Please execute the commands below, to start the process of stress:

* stress-ng --cpu N
    * start N workers continually writing, reading and removing temporary files.
* stress-ng --hdd N
* stress-ng --malloc N
* stress-ng --cache N

Where "N" means number of threads. 

*Before using intP command, you must open another tab in order to monitor the stressed resource.

Then, start intP command as root to monitor the executed application:
```shell
stap --suppress-handler-errors -g intp.stp stress-ng
```

```shell
Use the other tab to see the output with the following command:
watch -n2 -d cat /proc/systemtap/stap_*/intestbench
```

Examples:  

stress-ng --cpu 12
```shell
netp    nets    blk     mbw     llcmr   llcocc  cpu
0.00    0.00    0.00    0.00    0.00    0.83    0.50
```

stress-ng --hdd 5

```shell
netp    nets    blk     mbw     llcmr   llcocc  cpu
0.00    0.00    0.31    0.00    0.00    0.56    0.00
```

stress-ng --malloc 1

```shell
netp    nets    blk     mbw     llcmr   llcocc  cpu
0.00    0.00    0.00    0.10    0.08    0.51    0.07
```

stress-ng --cache 1

```shell
netp    nets    blk     mbw     llcmr   llcocc  cpu
0.00    0.00    0.00    0.00    0.05    0.89    0.07
```

These metrics represents the interference caused by the monitored application ( In this case stress-ng application): 

* netp - percentage of physical network
* nets - percentage of network queue interference.
* blk - percentage of disk interference.
* mbw - percentage of memory bus interference.
* llcmr - percentage of cache miss.
* llocc - percentage of cache interference.
* cpu - percentage of cpu interference.

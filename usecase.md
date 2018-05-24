---
layout: page
title: Using IntP with stress-ng application
permalink: /Experiments/
---

Stress−ng is a tool to load and stress a computer system. You can use it by downloading and installing with the follow command:

```shell
apt-get install stress-ng
```
In order to test most off all outputs data given by IntP, the follows command lines were used:

* stress-ng --cpu N
    * start N workers continually writing, reading and removing temporary files.
* stress-ng --hdd N
    * start N workers continually writing, reading and removing temporary files. The default mode is to stress test sequential writes and reads. 
* stress-ng --malloc N
    * start N workers continuously calling malloc.
* stress-ng --cache N
    * start N workers that perform random wide spread memory read and writes to thrash the CPU cache.

## Tests and Outputs

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

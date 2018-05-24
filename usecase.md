---
layout: page
title: Using IntP with stress-ng application
permalink: /Experiments/
---

**Stress−ng** is a tool that loads and cause stress into a a computer system or within an application. You can use it by downloading and installing to your system with the follow command:

```shell
apt-get install stress-ng
```
In order to test most of all data outputs given by IntP, the follows command lines were used:

* stress-ng --cpu N
    * start N workers continuously writing, reading and removing temporary files.
* stress-ng --hdd N
    * start N workers continuously writing, reading and removing temporary files. The default mode is to stress test sequential writes and reads. 
* stress-ng --malloc N
    * start N workers continuously calling malloc function.
* stress-ng --cache N
    * start N workers that performs random-wide spread memory read and writes to stress the CPU cache. 

## Tests and Outputs

The tests below were executed in a blade server PowerEdge M630 with 24 cores and 32 GB of memory. To execute all of our tests, we used 3 shell terminals. First with IntP command:

```shell
stap --suppress-handler-errors -g intp.stp stress-ng
```
 
 The second with output command:

```shell
watch -n2 -d cat /proc/systemtap/stap_*/intestbench
```
 
 The last terminal was used to run the application (stress-ng):

```shell
stress−ng [OPTION [ARG]] ...
```
 
## Results provided by our tool: 

**$ stress-ng --cpu 12**
```shell
netp    nets    blk     mbw     llcmr   llcocc  cpu
0.00    0.00    0.00    0.00    0.00    0.83    0.50
```

**$ stress-ng --hdd 5**

```shell
netp    nets    blk     mbw     llcmr   llcocc  cpu
0.00    0.00    0.31    0.00    0.00    0.56    0.00
```

**$ stress-ng --malloc 1**

```shell
netp    nets    blk     mbw     llcmr   llcocc  cpu
0.00    0.00    0.00    0.10    0.08    0.51    0.07
```

**$ stress-ng --cache 1**

```shell
netp    nets    blk     mbw     llcmr   llcocc  cpu
0.00    0.00    0.00    0.00    0.05    0.89    0.07
```

These metrics represents the interference caused by the monitored application (in this case stress-ng application): 

* netp - percentage of physical network
* nets - percentage of network queue interference.
* blk - percentage of disk interference.
* mbw - percentage of memory bus interference.
* llcmr - percentage of cache miss.
* llocc - percentage of cache interference.
* cpu - percentage of cpu interference.

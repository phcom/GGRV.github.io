---
layout: page
title: Installing stress-ng thourgh apt-get repository:
permalink: /Usecase/
---

```shell
apt-get install stress-ng
```
## Stress-ng tutorial using IntP:
Please execute the commands below, to start the process of stress:

* stress-ng --cpu 1&
* strees-ng --hdd 1&


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

stress-ng --cpu 1&
```shell
netp    nets    blk     mbw     llcmr   llcocc  cpu
0.00    0.00    0.00    0.00    0.00    0.00    0.99
```

stress-ng --hdd 2

```shell
netp    nets    blk     mbw     llcmr   llcocc  cpu
0.00    0.00    0.14    0.00    0.00    0.00    0.00
```
---
title: perf编译与使用
date: 2023-01-22 15:05:01
tags:
---
# perf编译与使用
- perf是一个linux内核自带强大的性能分析工具,不过有些系统里似乎不会将perf编译进去  
- 在Linux 2.6.31版本引入，至今tool/perf目录拥有1万多个提交，是内核开发中最活跃的几个领域之一。  
## 编译  
- 在大多数docker镜像中,似乎都没有带上这个强大的工具,所以需要自己手动编译(其实也能用apt安装,但是我没有成功过).  
- 首先需要知道自己系统的内核版本号, 输入`uname -r` 命令就能知道自己的内核版本号,然后根据内核版本号下载对应的linux源码,网址为: [linux kernel](https://cdn.kernel.org/pub/linux/kernel/).  
- 安装一些依赖:    
    ``` bash
    apt install flex
    apt install bison
    apt install zlib1g zlib1g-dev
    apt install libelf-dev
    apt install elfutils
    apt install systemtap-sdt-dev
    apt install libssl-dev
    apt install libunwind
    apt install libdw-dev
    apt install libcap-dev
    apt install libzstd-dev
    apt install binutils-dev
    apt install libiberty-dev
    apt install zlib-static
    apt install libslang2-dev
    apt install libunwind-dev
    apt install libperl-dev
    apt install libnuma-dev
    apt install libbabeltrace
    apt install libbabeltrace-dev
    apt install libbabeltrace-ctf-dev
    ```
- 然后进入下载的linux kernel源码目录编译安装perf  
    ```
    cd tools/perf
    make -j # 这一步请注意编译日志输出的perf的各个特性是否都开启了,如果没开启说明上面依赖安装不对
    make install
    cp perf /usr/bin
    ```
## 使用
``` bash
# 记录所有进程的耗时情况(函数的调用次数、热点函数...)
perf record -a

# 根据进程pid记录某个进程的耗时情况
perf record -p $PID

# 记录60s的进程数据
perf record -a sleep 60

# 记录程序调用堆栈
perf record -a -g

# 实时追踪当前系统的cpu使用情况
perf top
```
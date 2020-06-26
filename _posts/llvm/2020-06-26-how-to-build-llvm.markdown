---
layout: post
title:  "ubuntu16.04 搭建LLVM"
date:   2020-06-27 10:12:36
categories:  LLVM
---

* content
{:toc}


## 简介

在没有去实习之前，自己想找点事情做，于是就想着装一个LLVM，工作中可能会用到。我习惯使用ubuntu，我的ubuntu系统安装在虚拟机中，所以LLVM也是安装在虚拟机中。由于LLVM的编译过程使用到了较多磁盘，我给虚拟机分配的磁盘为20G，后面编译LLVM的时候提升磁盘空间不足，于是先解决了虚拟机磁盘空间不足的问题。其后接着编译LLVM，最后安装好LLVM。


## LLVM的安装
整个过程先下载相应源码，将部分源码移动到相应的文件夹下，然后创建build文件夹，等待编译完成。

### LLVM下载
在[LLVM官网](https://releases.llvm.org/)中，下载相应版本的压缩包，将其放在LLVM文件夹下，创建llvm文件夹，并将其解压到llvm。
### clang下载
同样在[LLVM官网](https://releases.llvm.org/)中下载对应的clang版本，将其解压到llvm/tools。
###Clang-extra-Tools下载
同样在[LLVM官网](https://releases.llvm.org/)中下载对应的Clang-extra-Tools版本，将其解压到llvm/tools/clang/tools，并重命名为extra。
###Compiler-RT下载
同样在[LLVM官网](https://releases.llvm.org/)中下载对应的Compiler-RT版本，将其解压到llvm/projects。
### 编译安装

    ①、在llvm同级目录下创建文件夹build，进入build目录。

    ②、以Release方式安装：  cmake -G "Unix Makefiles"      -DLLVM_ENABLE_ASSERTIONS=On -DCMAKE_BUILD_TYPE=Release ../llvm
    
    ③、make -jn，其中n取决于虚拟机所分配的cpu个数，我的虚拟机事先只分配了一个，速度较慢，如果是VM中安装的虚拟机可以在打开虚拟机的界面多分配几个，当然，编译过程时间不光是花费到CPU计算上，还有可能是磁盘IO。

    ④、sudo make install
## 使用
    确保安装完成，先在终端输入：clang --version，输出相应版本则无误。
      ①、使用clang编译c和cpp文件：clang <name>.cpp/<name>.c
      ②、使用clang将c和cpp文件编译为LLVM IR的二进制文件(.bc文件):clang -emit-llvm -c hello.c -o hello.bc
      ③、使用llvm虚拟机执行hello.bc:lli hello.bc
      ④、将.bc转为可读IR文件，即.ll文件：llvm-dis hello.bc

## 其它
    ①、由于llvm的交叉编译消耗很多磁盘，但是虚拟机在分配的时候只有20G，所以需要扩充磁盘。这里使用的工具是Gparted。
        a、首先在虚拟机开机界面，先设置好预分配的磁盘，然后开机进入系统。随后，打开Gparted，由于事先分配了多的磁盘，但是这些磁盘没有真正分配到虚拟机中，为了正确分配到虚拟机中。需要：
        首先将swap空间(交换空间)禁用(鼠标放到相应的条目右键，选择)，然后删除掉禁用后的swap分区，此时只剩下主分区和未分配的分区。
        然后在主分区上，将未分配空间增加进来，也是右键Resize，此后就剩下的未分配空间大大减少。
        在剩下未分配空间上新建扩展分区，文件系统选为：extended
        在上一步的扩展分区上创建逻辑分区，文件系统选为：linux-swap
        然后点击Gparted主界面上的"√"号，应用全部。
        分配完成后如下图：

        ![GParted](media/pics/Gparted.png)

    ②、后续内容是运行第一个LLVM提供的Pass例子。其后编写自己的Pass，并编译运行。
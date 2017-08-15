---
layout:            post
title:             "Install Mpich1.4 and ifort under Ubuntu system"
date:              2017-08-15 17:10:00 +0300
tags:              Mpich ifort Ubuntu installation
category:          Features
catalog:    		  true
header-img: 		  "img/post-bg-e2e-ux.jpg"
header-mask:       0.3
author:            Changhao Li
---

# Problem Discription

I need to compile some Fortran codes using MPI. However, Windows does not work because Mpich does not correctly support Windows. Then I installed VMware, and installed Ubuntu as virtual system. Then I need to install Mpich and ifort compiler in the Ubuntu virtual system. But some problems happened, the Mpich configuration program cannot recognize the ifort. 

```searching ifort... no```

But ifort has correctly installed in the system. I am beginner of Linux system, so I was very confused for this.

```
$ ifort -v
ifort version: xxxx
```

I searched this problem on the Internet, finally locked the solution and solved it. It was because under 64-bit Ubuntu system, some 32-bit packages are needed for the correct installation of ifort, but I omited this, and ifort cannot operate properly.

# Solution

When I was runnning the installation program of the Intel Parallel Studio XE(including ifort compiler), in the STEP5, this program checked the prerequisites of the installation. And such warning information is shown:

```
Missing optional prerequisites
-- 32-bit libraries not found
```
At the very beginning, I directly omitted this warning and continue the installation, because I thought 64-bit system should have good compatibility about 32-bit software. However, I was wrong. 32-bit packages were essential for the installation.

I checked the details of this warning information, and it showed:

```
One or more of these libraries could not be found:
	libstdc++ (including libstdc++6)
	glibc
	libgcc
```
Then common solution should be directly download and install these packages using apt-get.

```
$ sudo apt-get install libstdc++ glibc libgcc
```

However, it did not work because apt-get cannot find the libraries ```glibc``` and ```libgcc```.

```
E: Unable to locate package glibc
E: Unable to locate package libgcc
```

It got me confused again. I tried to google this error information, most people said that I should update the apt-get source.

```
$ sudo apt-get update
$ sudo apt-get upgrade
```

But after the apt-get updated, nothing happened, and ```glibc``` and ```libgcc``` still cannot be found.

Finally, I found the correct solution in the [**Ubuntu documentations**](https://help.ubuntu.com/community/InstallingCompilers). Here has sufficient instruction about all kinds of compilers. It is shown that 
:

*Using the Intel compilers for C, C++, and FORTRAN requires installing 32-bit libraries for Ubuntu if you are using a 64-bit system. Please ensuer you have these packages:*

```
1. gcc, build-essential, libc6-decv
2. ia32-libs, g++-multilib, and libc6-dev-i386(for 64-bit systems)
3. 32bit packages starting with lib32(for 64-bit systems)
4. alien and rpm for installing the RPM packages that intel distributes
5. libstdc++5 and libstdc++5-3.3-dev for good measure because Intel's builds depend on these runtimes.
```
*On 64-bit systems you may also need to issue these commands*

```
# cd /usr/lib32
# ln -s libpthread.so libpthread.so.0
.........
```

I installed all the depending packages and runned all commands as the instruction above. Then recheck the installation prerequisites, and the problems were finally solved.

By the way, during the installation of ```ifort```, I need to expand the root filesystem of ```Ubuntu```. This blog is very helpful. [How to expand the root filesystem of a 12.04 Ubuntu running inside VMware player](https://hexeract.wordpress.com/2012/04/30/how-to-expand-the-root-filesystem-of-a-11-10-ubuntu-running-inside-vmware-player)

# Summary

**1. the instructions and warnings of installation program should be fully noticed and respected, or some unexpected problems may happen, which could be very confusing and time-consuming.**

**2. The documentation and official instructions are far better than other information sources, which are best place to check problems and get started. Be patient to read them.**

**3. Finding solution online is a kind of essential job. Just like finding relevant literature.**
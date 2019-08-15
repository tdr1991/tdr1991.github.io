---
layout: post
title: 安装ubuntu18系统的wifi驱动
date: 2019-08-15
categories:
- ubuntu
- wifi
- driver
tags:
- 安装wifi驱动
---
安装ubuntu
<!--more-->


# 华硕笔记本ubuntu18.04安装wifi驱动

## 下载 backports-5.2-rc7-1.tar.gz

从 [这里](https://mirrors.edge.kernel.org/pub/linux/kernel/projects/backports/stable/) 下载 backports-5.2-rc7-1.tar.gz，一开始我下载的是 compat-drivers-3.7-rc1-6.tar.gz 但是有问题，提示说内核要在多少以上，初步怀疑是我的系统太高了，是ubuntu18.04,所以用了最新的。我是用U盘拷贝到电脑安装的，因为电脑无法连网，大部分软件从别的电脑或是手机下载的软件包。

## 开始安装
- 解压

```bash
tar xvf backports-5.2-rc7-1.tar.gz
```
- 切换目录
```bash
cd backports-5.2-rc7-1
```
- 编译
编译的时候提示没有配置，然后后面有些提示命令。
```bash
# make
make config-ath9k  #不确定
```
这条命令运行完后可能提示没有linux-headers和build-essential,linux-headers我是之前安装了，在 [中国科技大学](http://mirrors.ustc.edu.cn/) 下载的linux-headers-4.15.0-55-generic_4.15.0-55.60_amd64.deb，具体哪个目录不记得了。但是这两个deb可以去 [dkpg](https://pkgs.org/) 下载，应该可以不用版本都一样，后面的小版本可以不一样。
```bash
dkph -i linux-headers-4.15.0-55-generic_4.15.0-55.60_amd64.deb
dkpg -i build-essential_12.6_amd64.deb
```
如果权限不够就加 sudo 然后输入密码，输过一次就不用再输了。
中间可能还会遇到问题，比如我还安装了 libelf-dev_0.170-0.4_amd64.deb libelf1_0.170-0.4_amd64.deb 和 zlib1g-dev_1.2.11.dfsg-0ubuntu2_amd64.deb 这些包都在 [dkpg](https://pkgs.org/) 下载的。

- 安装
```bash
make install
```
我的提示还有密码之类问题，我猜测是说wifi的密码。所以当时没管，直接退出重启了。

- 退出
```bash
modprobe ath9k
exit
reboot
```

参考了(列个最重要的)
<https://blog.csdn.net/tonyjiang08/article/details/38400633/>

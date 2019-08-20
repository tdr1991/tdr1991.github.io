---
layout: post
title: 安装ubuntu
date: 2018-10-07
categories:
- ubuntu
tags:
- 安装系统
---
安装ubuntu
<!--more-->

# 华硕笔记本安装ubuntu
## 官网下载ubuntu
直接在ubuntu官网下载
## 制作U盘启动盘
- windows系统可以用 UltraISO
- ubuntu系统使用系统自带的 Startup Disk Creator
## 安装ubuntu
1. 设置U盘启动
开机一直按住 F2 进入 BIOS，在启动选项设置 U 为第一启动项，按 F10 保存退出启动。
2. 修改安装配置
在启动时，出现ubuntu选项后，按 e 进入编辑界面，找到 splash 其后添加 nouvearu.modeset=0 设置不用开源驱动，这是由于 nvidia 显卡与开源驱动不兼容，按 F10 启动安装。
3. 根据自己喜好进行安装
4. 安装 nvidia 驱动
- 安装驱动
```bash
sudo apt-get remove --purge nvidia* #删除所有的 nvidia 驱动
sudo ubuntu-drivers autoinstall #自动选择合适的驱动安装
nividia-smi #查看是否安装成功
```
- 彻底禁止 nouveau 
```bash 
sudo vi /etc/modprobe.d/blacklist-nouveau.conf 
# 插入以下两行内容
blacklist nouveau
options nouveau modeset=0
```
5. 安装搜狗拼音
```bash
# 安装 fcitx 框架
sudo apt install fcitx-table-wbpy fcitx-config-gtk
# 切换 fcitx 输入法
im-config -n fcitx
# 官网下载 linux 版 sogoupinyin
# 安装软件，使用 dpkg 安装deb
```
如果还没出来搜狗拼音输入法，那么点击右上角的键盘图标，点击配置输入法，在输入法选项卡下面点击+号，去掉只显示当前语言的勾，把搜狗拼音添加进去，不出意外就能显示了。
6. shell忽略大小写敏感
```bash
sudo vi ~/.inputrc 
#在该文件添加以下内容
set completion-ignore-case on

"\e[A": history-search-backward
"\e[B": history-search-forward
```
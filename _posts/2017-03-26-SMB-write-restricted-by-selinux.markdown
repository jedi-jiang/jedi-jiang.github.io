---
layout: post
title:  "一个奇怪的SMB权限问题"
date:   2017-03-26 21:50:00 +0800
categories: 坑你没商量
tags:   SMB SELinux 随记
---

上周五(2017-03-24)同事反应，一台SMB服务器在重启后，原来有写入权限的帐户均变为只读权限，找不到原因。
经查看 `/etc/samba/smb.conf` 发现配置没有问题，重启SMB服务，问题依旧。后来同事查阅网上资料，可能和SELinux有关，将selinux关闭后，问题现象果然消失了。


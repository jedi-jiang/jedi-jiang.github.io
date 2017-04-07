---
layout: post
title:  "解决使用jgit时出现ssh算法协商失败的问题"
date:   2017-04-07 21:40:00 +0800
categories: Git
tags:  Git
---

今天尝试使用jgitflow，在开启`enableSshAgent`后，执行 `mvn jgitflow:release-start` 时出现异常，报错：Algorithm negotiation fail。
该问题在之前使用EGit插件时也出现过，根据stackoverflow上的资料，在将以下内容添加到GitLab服务器上的`/etc/ssh/sshd_config`文件中后，问题即得到解决。
> `KexAlgorithms curve25519-sha256@libssh.org,ecdh-sha2-nistp256,ecdh-sha2-nistp384,ecdh-sha2-nistp521,diffie-hellman-group-exchange-sha256,diffie-hellman-group14-sha1,diffie-hellman-group-exchange-sha1,diffie-hellman-group1-sha1`

但今天将上述内容加入后，问题依旧，于是继续查找资料，最终确认，还需将下述内容添加到`/etc/ssh/sshd_config`文件后才能彻底解决该问题。
> `MACs hmac-sha2-512-etm@openssh.com,hmac-sha2-256-etm@openssh.com,hmac-ripemd160-etm@openssh.com,umac-128-etm@openssh.com,hmac-sha2-512,hmac-sha2-256,hmac-ripemd160,umac-128@openssh.com,hmac-md5,hmac-sha1,hmac-sha1-96,hmac-md5-96`

该问题应该与jsch库以及服务器端的OpenSSH Server版本有关，版本不同，可能配置上会有差异，在出现类似问题时应予以注意。

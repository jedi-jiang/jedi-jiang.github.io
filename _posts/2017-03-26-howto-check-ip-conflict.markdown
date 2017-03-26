---
layout: post
title:  "如何检测IP冲突"
date:   2017-03-26 23:01:00 +0800
categories: 运维
tags:   网络管理 随记
---

不久前，一台装有项目管理软件的服务器突然无法访问使用，直接在服务器上操作一切正常，因此判断服务器IP有冲突，在Google上查阅了使用命令检测IP冲突的方法，现记录一下，以备后查。

{% highlight bash %}
# Linux
arping -D -c 2 xxx.xxx.xxx.xxx
echo $? # 0 表示有冲突，1表示没有冲突

# OS X
arping xxx.xxx.xxx.xxx
# 如果输出结果中有一个以上的MAC地址，则说明有冲突
{% endhighlight %}



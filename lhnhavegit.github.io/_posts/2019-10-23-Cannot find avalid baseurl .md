---
layout: post
categories:
  - ACM
  - Template
tags: Linux
date: 2019-10-22 12:28:11
---

##centos7使用yum安装软件提示 cannot find a valid baseurl for repo:base/7/x86_64 的解决方法
由于是本地yum源安装软件，无法联网，因此使用yum安装软件时报了错，解决方法是：

打开vi /etc/resolv.conf文件 把里面的内容改成：

nameserver 8.8.8.8  

修改完之后，需要重启网卡

centos6的网卡重启方法：service network restart

centos7的网卡重启方法：systemctl restart network

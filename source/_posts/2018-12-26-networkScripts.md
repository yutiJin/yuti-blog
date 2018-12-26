---
title: Linux的网络桥接模式
date: 2018-12-26 12:51:59
categories:
- WORK
- Linux
---

> 我的理解：
> 
> 桥接模式：虚拟机与本机使用不一样的ip，外网可以访问虚拟机
> 
> NAT模式：虚拟机和本机公用一个ip，外网不能访问虚拟机


下面介绍桥接模式的配置

## 适配器选择桥接模式

CenterOs 7 中网络适配器选择桥接模式
![桥接模式选择](http://pic.yuti.site/bridgeModel.png)

## 网卡地址修改

1、cmd查看本地的DNS

```
ipconfig /all
```
或者以下方式进行查看
![img](http://pic.yuti.site/DNS.png)


2、linux中通过以下命令进入编辑区

```
vi /etc/sysconfig/network-scripts/ifcfg-ens32
```

设置静态ip（添加如下语句）    

```
BOOTPROTO=“static”

IPADDR=192.168.11.58     //根据本地的IP进行设置，就前三位要与本地IP相同

NETMASK=255.255.255.0

GATEWAY=192.168.11.1

DNS1=10.11.248.114      //根据下图进行选择（这个必须对，不让就上不了网）
                        //下面的246就是错的，因为这个错误我不能ping通baidu，
                        //浪费了不少时间，这一定要注意
```

![img](http://pic.yuti.site/DNS1.png)

3、查看虚拟网络编辑是否合理
![](http://pic.yuti.site/AutoBridgeModel.png)

4、重启

```
service network restart

or

/etc/init.d/network restart
```


到这里其实就可以结束了，虚拟机桥接模式上网以及没有问题了。

以下步骤看自己需要

## Xshell

Xshell：在Windows系统下可以用来远程访问不同系统下的服务器

> 我的理解：
> 
> 优点：轻量、能够同时连接并操作多台虚拟机



1、centos安装ssh server

```
# 安装
sudo yum install openssh-server

# 启动
sudo systemctl enable sshd
sudo systemctl start  sshd

# 开放ssh的端口  默认22
iptables -A INPUT -s 192.168.11.0/24 -p tcp --dport 22 -j ACCEPT

```

2、打开下载好的Xshell，然后配置虚拟机的IP（192.168.11.158）

![添加新的被控器](http://pic.yuti.site/Xshell.png)


3、如果不能ping成功，则把Windows和虚拟机的防火墙都删掉

```
# 虚拟机关闭防火墙
systemctl stop firewalld.service    //停止firewall

systemctl disable firewall.service   //禁止firewall开机启动
```

> That's all, over!
> 
> 听的再多都不如实际操作，在听老师讲的时候，都没有遇见过什么奇怪的问题，也不知道自己哪里不懂，感觉自己全知道，so easy！但是到实际操作的时候就会遇见各种奇葩的问题，还不知道怎么下手，怎么问度娘，经过两个晚上的折磨还好是弄出来了。在解决bug的过程中，恩，比以前更加深刻的理解了linux。棒棒哒
> 
> bug：虚拟机能ping通本地，但是ping不同www.baidu.com
> 
> answer: DNS出错
> 
> 注释：主机名解析不对，一般都是DNS出错





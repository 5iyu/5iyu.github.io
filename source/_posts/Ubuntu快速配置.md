---
title: Ubuntu快速配置
date: 2024-06-08 21:51:00
categories: 环境配置
tags:
  - Ubuntu
---
ubuntu的快速使用配置
<!-- more -->

## windows关闭Hyper-V 
win不关闭Hyper-V，会导致虚拟机运行卡机。
超详细讲解win10 Hyper-V 关闭(禁用)方法
[https://blog.csdn.net/weixin_46706771/article/details/107991229](https://blog.csdn.net/weixin_46706771/article/details/107991229)

## 安装ware
很多资源站都有

## 下载Ubuntu镜像
[ISCAS镜像站](https://mirror.iscas.ac.cn/ubuntu-releases/23.10/)

## ware配置镜像启动
1. 选择经典安装
2. 选择 稍后安装操作系统
3. 选择 Linux - ubuntu
4. 最大磁盘空间 100G - 将虚拟磁盘拆分为多个文件
5. 自定义硬件
   - 内存 4g
   - 网络 桥接
   - 使用ISO镜像文件 - 启动完成切换为使用物理驱动器
   - 处理器默认
   - 取消显示器3D加速
  
## Ubuntu启动配置
[【Linux】Ubuntu23.10+VMWare17虚拟机的安装教程 -  CSDN App]http://t.csdnimg.cn/thHDl

根据此教程选择即可，其实也没什么特别选项。网上的教程很多，但是试错比较麻烦。作者这样子配置，自己配置的时候不一定能行。


## 使用中文输入
![20240608234545](https://s2.loli.net/2024/06/08/5CXabrDudRhIH8G.png)

## 切换apt软件源
方法一：图形界面配置
start - 设置 - 软件和更新 - 下载自 - 其它 - 中国 - 选择镜像源 - 关闭 - 更新 - end
方法二：命令行配置
网上搜索即可
方法三：直接修改配置文件
同同上

## 查看ip和路由
```bash
ifconfig
route -n
```
如果没有安装则：
```bash
sudo apt update -y 
sudo apt install net-tools -y 
```

## shell远程连接
1. Ubuntu安装ssh服务
```bash
sudo apt install openssh-server
```
2. 下载Nxshell客户端
    - 切换中文语言
![20240608235433](https://s2.loli.net/2024/06/08/IOiBvy1nqXfKjAU.png)
    - 配置连接信息，配置ip 和登录名密码即可

ok，基本配置完成，可以进行使用了。
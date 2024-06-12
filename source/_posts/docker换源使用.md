---
title: docker换源使用
date: 2024-06-09 19:58:27
categories: 环境配置
tags: 
- docker
- 换源
---
切换docker源就可以拉取了，国内好新人还是多的
<!-- more -->
## 切换docker源
```bash
sudo vim /etc/docker/daemon.json
```
下面的步骤不执行也能使用
重新加载json配合配置文件
```
sudo systemctl daemon-reload
```
重启docker
```bash
sudo systemctl restart docker
```
以上是网友自建分享的，使用不了多久
## 使用阿里云转存镜像
up 技术爬爬虾分享了阿里云转存镜像的教程视频，解决国内无法使用docker的问题

现在全面封锁，阿里估计也上不了什么大分。

暂时能用也是一种有效的解决方案

## Ubuntu安装docker
切换apt源
```
sudo apt-get install ca-certificates curl
curl -fsSL http://mirrors.aliyun.com/docker-ce/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] http://mirrors.aliyun.com/docker-ce/linux/ubuntu $(lsb_release -cs) stable"
sudo apt-get install docker-ce docker-ce-cli containerd.io
```
测试成功
![20240609204506](https://s2.loli.net/2024/06/09/i2x7vGRTLhVEUWO.png)

安装如此简单？离线的方式有空再研究一下，现在先这样用着
![20240609204739](https://s2.loli.net/2024/06/09/NTv91KrCikJRLgB.png)

## docker镜像源
20240609 拉取失败
Daocloud
```bash
https://registry.daocloud.io/
```

网友自建
```bash
https://registry.moslb.com
```
拉取超时，没什么用。

## 试一下转存
跟着配置没什么问题，可是拉取到我就不行了，每一件事是顺利的。
![20240609213152](https://s2.loli.net/2024/06/09/sAYXjZItqJaiveU.png)


吓我一跳，多拉几次就成功了。
这个镜像是设置公开的。下面实现私有的这么设置。
![20240609221500](https://s2.loli.net/2024/06/09/5xEdVKlh29Hrnce.png)


私有的也是要哆啦几次才行，后面还加上了版本号，这个版本号不知道重不重要。
![20240609222254](https://s2.loli.net/2024/06/09/kPdGErv1NBJQAYl.png)

拉跨，本来还以为能够使用了，要么是拉取不下，要么还是拉取不下来。

收工。

一个镜像要拉好久

![20240609234628](https://s2.loli.net/2024/06/09/krVShJmYWn5qX6D.png)


https://mirror.baidubce.com

sudo mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<-'EOF'
{
    "registry-mirrors": [
        "https://docker.m.daocloud.io"
    ]
}
EOF
sudo systemctl daemon-reload
sudo systemctl restart docker
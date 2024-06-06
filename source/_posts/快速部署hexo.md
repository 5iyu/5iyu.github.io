---
title: 快速部署hexo
date: 2024-06-06 18:21:40
categories: hexo
tags:
- 主题
- 部署
- hexo
---

Hexo 是一个快速、简洁且高效的博客框架。Hexo 使用 Markdown（或其他标记语言）解析文章，在几秒内，即可利用靓丽的主题生成静态网页。
<!-- more -->
## 安装nodejs
[官网下载](https://nodejs.org/en/)
## 安装hexo
安装好hexo后，在命令行中输入`hexo -v`查看版本号，若出现版本号则说明安装成功。  
本地安装hexo完成。
```bash
npm install hexo-cli -g
hexo init blog
cd blog
npm install
hexo server
```
基本使用命令
```bash
hexo new "postName" #新建文章
hexo new page "pageName" #新建页面
hexo generate #生成静态页面
hexo server #开启预览访问端口（默认端口4000，如已占用可修改_config.yml文件port配置）
hexo deploy #将.deploy文件夹部署到GitHub
```
## 配置站点文件
url 配置成自己的域名，否则会出现404错误。

配置git同步信息
```
deploy:
    type: git
    repo: git@github.com:5iyu/5iyu.github.io.git
    branch: master
```
hexo同步需要安装hexo-deployer-git
```
npm install hexo-deployer-git --save
```
站点修改中文
```
language 后面输入 zh-CN。
```

## 配置next主题
安装主题
```bash
git clone https://github.com/theme-next/hexo-theme-next themes/next
```
安装完成后，打开 Hexo 配置文件并将theme变量设置为next
```
theme: next
```
标签和分类在menu中，需要手动开启
```
menu

切换主题
# Schemes
scheme: Muse
#scheme: Mist
#scheme: Pisces
#scheme: Gemini
选择你喜欢的一种样式，去掉前面的 #，其他主题前加上 # 即可
```
## 开启分类标签功能
在source目录中会生成相关的文件，在index.md中添加type: "categories"和type: "tags"，分别对应分类和标签。
```
hexo new page categories
hexo new page tags
```
scaffolds文件夹中修改生成模板
```
---
title: md.md
date: 2024-06-06 18:21:40
categories:
tags:
---
```
## 浏览页面显示当前浏览进度
打开 themes/next/_config.yml，搜索关键字 scrollpercent，把 false 改为 true。
![](https://img-blog.csdnimg.cn/20190829154043665.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2FzNDgwMTMzOTM3,size_12,color_FFFFFF,t_70)

## 开启复制
搜索 codeblock，找到如下配置
```
codeblock:
border_radius: 8   # 按钮圆滑度
copy_button:  # 设置是否开启代码块复制按钮
	enable: true
	show_result: true  # 是否显示复制成功信息

```
## 文章加密
[插件地址](https://github.com/D0n9X1n/hexo-blog-encrypt)
安装插件
```bash
npm install hexo-blog-encrypt
```
在主题文件_config.yml中启用插件
```
# 文章加密 hexo-blog-encrypt
# Security
encrypt: # hexo-blog-encrypt
  abstract: 这是加密的东西，继续阅读需要密码。
  message: 嘿，这里需要密码。
  tags:
  - {name: encryptAsDiary, password: passwordA}
  - {name: encryptAsTips, password: passwordB}
  wrong_pass_message: Oh, this is an invalid password. Check and try again, please.
  wrong_hash_message: Oh, these decrypted content cannot be verified, but you can still have a look.
```
文章添加加密标签，例如
```
---
title: hexo加密1
date: 2024-06-06 18:21:40
categories: hexo
tags:
- 主题
- 部署
- hexo
password: 123 
---
```

## 开启本地搜索
安装插件
```
npm install hexo-generator-searchdb --save
```
在主题文件_config.yml中启用插件
```
# Local search
local_search:
    enable: true
```
本地不是基本完成
## 部署到github
1. 新建一个仓库，名字为：github用户名.github.io
2. 配置git公钥上传到github的setting -> ssh中
3. hexo g -d 编译静态网页并上传到github仓库
4. 设置github仓库的setting -> github pages -> source 选择 master branch
5. 访问github用户名.github.io

首次使用git需要配置用户名和邮箱
```bash
git config --global user.name "username"
git config --global user.email "<EMAIL>"
```
生成ssh公钥，在命令行中输入
```bash
ssh-keygen -t rsa -C "<EMAIL>"
```
在.ssh文件夹中生成id_rsa和id_rsa.pub文件，将id_rsa.pub文件内容复制到github setting ->
电脑路径
```bash
C:\Users\Administrator\.ssh
```
将生成的id_rsa.pub文件内容复制到github setting -> ssh中

## 备份hexo源码
通过git分支的方式备份，使用那个备份插件上传的还是静态网页。

1. 首先把github仓库克隆到本地，复制.git文件夹到hexo根目录

2. 创建.gitignore文件
```
# .gitignore
.DS_Store
Thumbs.db
db.json
*.log
node_modules/
public/
.deploy*/
.git*/
# 这里只备份主题的配置文件
.vscode/
```
3. 创建分支
```bash
git branch -a
# 查看所有分支

git branch 
# 查看当前使用分支

git branch -b hexo-backup
# 切换到 hexo_backup 分支上，若不存在则创建该分支并切换到该分支

# git branch -d hexo_backup
# 删除本地 hexo_backup 分支

# git push origin --delete hexo_backup
# 删除远程 hexo_backup 分支
```

## 提交备份
```
git add .
# 添加当前目录

git commit -m "backup"
# 添加commit，引号内的内容随意

# 添加远程源
git remote add origin <EMAIL>:5iyu/5iyu.github.io.git

# 切换远程源
git remote set-url origin <EMAIL>:5iyu/5iyu.github.io.git

git push origin hexo_backup
# 将本地数据推送到 hexo_backup 分支中
```
备份完成
## 恢复备份
新环境配置
```bash
npm install -g hexo-cli
hexo init
```
克隆备份分支
将原来的source, package.json等文件克隆到hexo根目录下
```
git clone -b hexo_backup git@github.com:[username]/[username].github.io.git
npm install
```

渲染与推送
```bash
hexo clean
hexo g -d
```
主分支利用hexo自身集成的git组件进行推送。

网络教程很多，但是很多都是有问题的，这里记录一下正确的步骤。

使用·`hexo g -d`同步到github总是有点问题，多同步几次就好了。

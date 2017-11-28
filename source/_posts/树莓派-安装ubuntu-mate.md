---
title: 树莓派 安装ubuntu mate
date: 2017-11-28 14:47:51
tags: [pi,树莓派]
---

## 设置root密码
```
linuxidc@ubuntu:~$ sudo passwd
[sudo] password for linuxidc: 
输入新的 UNIX 密码： 
重新输入新的 UNIX 密码： 
passwd：已成功更新密码
linuxidc@ubuntu:~$
```

## vi 使用不习惯
>问题分析：ubuntu预装的是vim tiny版本，   
>而常用的是vim full版本。执行下面的语句安装vim full版本：

* 卸载`vim-common`   
```bash
sudo apt-get remove vim-common
```
* 安装`vim`   
```bash
sudo apt-get install vim
```

## 修改Ubuntu的`apt-get`源为阿里源的方法
1、复制原文件备份
```bash
sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak
```
2、编辑源列表文件
```bash
sudo vim /etc/apt/source.list
```
3、将原来的列表删除，添加如下内容
```bash
deb http://mirrors.aliyun.com/ubuntu/ vivid main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ vivid-security main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ vivid-updates main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ vivid-proposed main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ vivid-backports main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ vivid main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ vivid-security main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ vivid-updates main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ vivid-proposed main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ vivid-backports main restricted universe multiverse
```
4、运行`sudo apt-get update`

## git 
```bash
sudo apt-get install git
```
## zsh

```bash
sudo apt-get install zsh
zsh --version
sudo chsh -s `which zsh`
#注销重新登录
sudo reboot
```
* 再次连接
```bash
cp ~/.zshrc ~/.zshrc.orig
cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc
vi ~/.zshrc
```
* 配置zsh
```bash
ZSH_THEME="random" # (...please let it be pie... please be some pie..)
disable_auto_update = true
source ~/.zshrc
```
* 如果你想在任何时间点升级（也许有人刚刚发布了一个新的插件，你不想等待一个星期？)你只需要运行：
```bash
upgrade_oh_my_zsh
```

* 安装oh-my-zsh   
```bash
git clone git://github.com/robbyrussell/oh-my-zsh.git ~/.oh-my-zsh
```
## 安装ssh

* 安装openssh-server
```bash
sudo apt-get install openssh-server
```
* 查看openssh-server是否启动
```bash
ps -e | grep ssh
```
* 启动、停止和重启openssh-server的命令如下
```bash
/etc/init.d/ssh start
/etc/init.d/ssh stop
/etc/init.d/ssh restart
```
* 配置openssh-server   
openssh-server配置文件位于`/etc/ssh/sshd_config`，   
在这里可以配置SSH的服务端口等，例如：默认端口是22，可以自定义为其他端口号，如222，然后需要重启SSH服务。

* Ubuntu中配置openssh-server开机自动启动   
打开`/etc/rc.local`文件，在`exit 0`语句前加入：
```bash
/etc/init.d/ssh start
```

5、运行`sudo apt-get upgrade`

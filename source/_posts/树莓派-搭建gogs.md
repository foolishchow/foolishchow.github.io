---
title: 树莓派 搭建gogs
date: 2017-11-28 14:54:24
tags: [pi,树莓派,gogs]
---
# gogs 安装


## mysql
```bash
sudo apt-get install mysql-server
sudo apt-get install mysql-client
sudo apt-get install libmysqlclient-dev
```

```bash
sudo netstat -tap | grep mysql
mysql -u root -p
```
* 配置用户

```
# default-storage-engine=INNODB
show engines;
show variables like '%storage_engine%';


CREATE DATABASE gogs CHARACTER SET utf8 COLLATE utf8_bin;
GRANT ALL PRIVILEGES ON gogs.* TO 'root'@'localhost' IDENTIFIED BY 'root';
FLUSH PRIVILEGES;
QUIT；
```

```bash
sudo adduser git

su git
cd ~
wget https://dl.gogs.io/0.11.29/raspi2_armv6.zip
unzip linux_amd64.zip
```
> 安装过程中会提示你输入一些密码，
> 这里最好把自己输入的内容全部记下来，防止忘记，不然密码忘了就废了。    


## 可能遇到的问题

> fatal: the remote end hung up unexpectedly 

发生在push命令中，有可能是push的文件过大导致
* 解决方法：
  * windows:   
  在 .git/config 文件中加入
  ```[http]
  postBuffer = 524288000
  ```
  * linux:
  ```
  git config http.postBuffer 524288000
  ```

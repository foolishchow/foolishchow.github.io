---
title: 树莓派 安装node环境
date: 2017-11-28 14:56:36
tags: [pi,树莓派,node]
---

# node 环境搭建

## nvm

* 依赖
```bash
sudo apt-get update  
sudo apt-get install build-essential libssl-dev 
```
* nvm
```
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.6/install.sh | bash
source ~/.zshrc
```

* 修改源
```bash
vi ~/.zshrc
```
	输入
	```
	export NVM_NODEJS_ORG_MIRROR="https://npm.taobao.org/mirrors/node"
	export NVM_IOJS_ORG_MIRROR="http://npm.taobao.org/mirrors/iojs"
	```


## node相关的源
```bash
vi ~/.zshrc
```
输入
```
move_to_trash () {
    new_name=`date "+%y-%m-%d_%H_%M_%S"`
    mv "$@" ~/.Trash/"$@ $new_name"
}
alias trash='move_to_trash'
export ELECTRON_MIRROR="https://npm.taobao.org/mirrors/electron/"
export SASS_BINARY_SITE="http://npm.taobao.org/mirrors/node-sass"
export SQLITE3_BINARY_SITE="http://npm.taobao.org/mirrors/sqlite3"
export PHANTOMJS_CDNURL="https://npm.taobao.org/mirrors/phantomjs/"
export CHROMEDRIVER_CDNURL="https://npm.taobao.org/mirrors/chromedriver"
export SELENIUM_CDNURL="https://npm.taobao.org/mirrorss/selenium"
export NPＭ_CONFIG_REGISTRY="https://registry.npm.taobao.org"
```

## 问题   
* `libssl-dev`   

> The following packages have unmet dependencies:
 libssl-dev : Depends: libssl1.0.0 (= 1.0.2g-1ubuntu4) but 1.0.2g-1ubuntu4.6 is to be installed
  Recommends: libssl-doc but it is not going to be installed
E: Unable to correct problems, you have held broken packages.
  
    

* 原因      
已安装的libssl1.0.0版本太高, 无法支持   
* 解决方案:   
使用aptitude软件包管理器
1. 安装aptitude
```bash
sudo apt-get install aptitude
```
2. 使用aptitude安装 libssl-dev包, 采用建议的解决方案(将libssl1.0.0版本降级)
```
sudo aptitude install libssl-dev
```

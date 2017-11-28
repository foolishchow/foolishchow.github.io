---
title: 树莓派 安装ffmpeg
date: 2017-11-28 14:52:15
tags: [pi,树莓派,ffmpeg]
---
# 安装ffmpeg

## 安装各种解码器

* lame
```bash
wget https://jaist.dl.sourceforge.net/project/lame/lame/3.99/lame-3.99.5.tar.gz
tar -zxvf lame-3.99.5.tar.gz
cd lame-3.99.5 
./configure --enable-shared
make 
make install
```

* libogg
```bash
wget http://downloads.xiph.org/releases/ogg/libogg-1.3.2.tar.gz
tar -zxvf libogg-1.3.2.tar.gz
cd libogg-1.3.2
./configure --enable-shared
make 
make install
```

* libvorbis
```bash
#libvorbis依赖于libogg, 所以libogg必须先于libvorbis安装
wget http://downloads.xiph.org/releases/vorbis/libvorbis-1.3.5.tar.gz
tar -zxvf libvorbis-1.3.5.tar.gz
cd  libvorbis-1.3.5
./configure --enable-shared
make 
make install
```

* xvidcore
```bash
wget http://downloads.xvid.org/downloads/xvidcore-1.3.2.tar.gz
tar -zxvf xvidcore-1.3.2.tar.gz 
cd xvidcore/build/generic
./configure --enable-shared
make 
make install
```

* x264
```bash
last_x264.tar.bz2包
因为没有找到好的资源，给一个ftp资源，下载最新版本之后上传到linux上
ftp://ftp.videolan.org/pub/videolan/x264/snapshots/
tar -jxvf last_x264.tar.bz2
cd x264-snapshot-20170330-2245
./configure --enable-shared
make 
make install
```

* libdts
```bash
wget http://down1.chinaunix.net/distfiles/ffmpeg-0.5.tar.bz2
tar -jxvf libdca-0.0.5.tar.bz2
cd libdca-0.0.5
./configure --enable-shared
make 
make install
```
* faad2
```bash
wget https://jaist.dl.sourceforge.net/project/faac/faad2-src/faad2-2.7/faad2-2.7.tar.gz
tar -zxvf faad2-2.7.tar.gz
cd faad2-2.7
./configure --enable-shared
make 
make install
```
* faac   
```bash
wget https://jaist.dl.sourceforge.net/project/faac/faac-src/faac-1.28/faac-1.28.tar.gz
tar -zxvf faac-1.28.tar.gz
cd faac-1.28
./configure --enable-shared
make 
make install
```

> 编译FAAC-1.28时遇到错误
[mpeg4ip.h:126: error: new declaration ‘char* strcasestr(const char*, const char*)’]
找到mpeg4ip.h并修改修改

```bash

解决方法：
从123行开始修改此文件mpeg4ip.h，到129行结束。
修改前：
#ifdef __cplusplus
extern "C" {
#endif
char *strcasestr(const char *haystack, const char *needle);
#ifdef __cplusplus
}
#endif

修改后：
#ifdef __cplusplus
extern "C++" {
#endif
const char *strcasestr(const char *haystack, const char *needle);
#ifdef __cplusplus
}
#endif
```
* amr-nb
```bash
wget http://ftp.penguin.cz/pub/users/utx/amr/amrnb-10.0.0.0.tar.bz2
tar -jxvf amrnb-10.0.0.0.tar.bz2
cd amrnb-11.0.0.0
./configure --enable-shared
make 
make install
```
* amr-wb
```bash
wget http://ftp.penguin.cz/pub/users/utx/amr/amrwb-11.0.0.0.tar.bz2
tar -jxvf amrwb-11.0.0.0.tar.bz2
cd amrwb-11.0.0.0
./configure --enable-shared
make 
make install
```

## 安装yasm
```bash
#ffmpeg编译中为了提高编译速度，使用了汇编指令，于是需要使用这个工具。
yum -y install yasm

```

## 安装ffmpeg
```bash
wget http://ffmpeg.org/releases/ffmpeg-3.2.4.tar.bz2
tar -jxvf http://ffmpeg.org/releases/ffmpeg-3.2.4.tar.bz2
cd ffmpeg-3.2.4
#其中–enable-shared表示生成动态链接库，可以供以后编程使用，同时生成的可执行程序也依赖这些动态库。如果不加上–enable-shared选项则使用静态链接的方式编译，此时不会生成动态库，同时生成的ffmpeg等的可执行文件也比较大，但他们不需要动态库就可以直接运行
./configure --enable-shared
#编译，需要较长时间，10分钟左右。
make
#安装
make install
#安装完成后
vi /etc/ld.so.conf.d/
把/usr/local/ffmpeg/lib填写到该文件中
再执行ldconfig，更新ld.so.cache，使修改生效。
#测试安装是否成功
cd /usr/local/ffmpeg/bin
#执行
./ffmpeg
#出现如下内容说明安装成功
ffmpeg version 3.2 Copyright (c) 2000-2016 the FFmpeg developers
  built with gcc 4.4.7 (GCC) 20120313 (Red Hat 4.4.7-17)
  configuration: --enable-shared --prefix=/usr/local/ffmpeg
  libavutil      55. 34.100 / 55. 34.100
  libavcodec     57. 64.100 / 57. 64.100
  libavformat    57. 56.100 / 57. 56.100
  libavdevice    57.  1.100 / 57.  1.100
  libavfilter     6. 65.100 /  6. 65.100
  libswscale      4.  2.100 /  4.  2.100
  libswresample   2.  3.100 /  2.  3.100
Hyper fast Audio and Video encoder
usage: ffmpeg [options] [[infile options] -i infile]... {[outfile options] outfile}...

Use -h to get full help or, even better, run 'man ffmpeg'
```
## 使用ffmpeg转换视频
```bash
#ffmpeg常用参数的介绍
#-i 指定要转换视频的源文件
#-s 视频转换后视频的分辨率
#-vcodec 视频转换时使用的编解码器
#-r 视频转换换的桢率(默认25桢每秒)
#-b 视频转换换的bit率
#-ab 音频转换后的bit率(默认64k)
#-acodec 制度音频使用的编码器
#-ac 制定转换后音频的声道
#-ar 音频转换后的采样率
./ffmpeg -i source.wmv 
-f psp -r 29.97 -b 768k -ar 24000 -ab 64k -s 320*240 destination.mp4
```



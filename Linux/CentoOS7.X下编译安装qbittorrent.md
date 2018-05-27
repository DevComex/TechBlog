首先从下述页面获取下载链接：
https://www.qbittorrent.org/download.php
我们得到Tar.gz的链接为：
https://sourceforge.net/projects/qbittorrent/files/qbittorrent/qbittorrent-4.1.0/qbittorrent-4.1.0.tar.gz/download
更换其中的版本为3.3.11
https://sourceforge.net/projects/qbittorrent/files/qbittorrent/qbittorrent-3.3.11/qbittorrent-3.3.11.tar.gz/download
### 通过浏览器打开页面获取下载地址
```
wget https://excellmedia.dl.sourceforge.net/project/qbittorrent/qbittorrent/qbittorrent-3.3.11/qbittorrent-3.3.11.tar.gz
```
https://github.com/DevComex/TechBlog/blob/master/ScreenShots/ScreenShot-2018-05-27_120126.png

### 解压文件
```
tar -zxf qbittorrent-3.3.11.tar.gz
```
https://github.com/DevComex/TechBlog/blob/master/ScreenShots/ScreenShot-2018-05-27_120526.png

### 依赖项安装配置
首先需要安装GCC
```
yum install gcc -y
```
安装qt-devel
```
yum install qt-devel -y
```
添加QT4路径到环境变量（修改/etc/profile）
```
QTDIR=/usr/lib64/qt4
PATH=$PATH:$HOME/bin:$QTDIR/bin
export PATH QTDIR
```
最后重新登陆Linux,使其生效
```
exit
```
安装依赖项boost-devel
```
yum install boost boost-devel -y
```
安装依赖项libtorrent-rasterbar
```
yum install openssl-devel
wget https://github.com/arvidn/libtorrent/releases/download/libtorrent-1_1_7/libtorrent-rasterbar-1.1.7.tar.gz
tar -zxf libtorrent-rasterbar-1.1.7.tar.gz
cd libtorrent-rasterbar-1.1.7/
./configure --disable-debug --prefix=/opt/libtorrent --with-boost-libdir=/usr/lib64
make
make install
```
因为安装在非默认目录，我们还需要设置环境变量
```
export libtorrent_CFLAGS=/opt/libtorrent/include/libtorrent/
export libtorrent_LIBS=/opt/libtorrent/lib/
```

### Installation:
For installation, follow the instructions from INSTALL file, but simple:

```
cd qbittorrent-3.3.11
./configure --prefix=/opt/qbittorrent --with-qt4
![](https://github.com/DevComex/TechBlog/blob/master/ScreenShots/ScreenShot-2018-05-28_074739.png)
make && make install
qbittorrent
```
在执行make时会遇到如下错误
```
cd src/ && make -f Makefile 
make[1]: 进入目录“/root/qbittorrent-3.3.11/src”
compiling app/qtsingleapplication/qtsingleapplication.cpp
g++: 致命错误：当有多个文件时不能在已指定 -c 或 -S 的情况下指定 -o
编译中断。
make[1]: *** [qtsingleapplication.o] 错误 4
make[1]: 离开目录“/root/qbittorrent-3.3.11/src”
make: *** [sub-src-make_default] 错误 2
```

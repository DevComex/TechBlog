### 下载安装介质
通过浏览器打开页面获取下载地址
```
wget https://downloads.sourceforge.net/project/qbittorrent/qbittorrent/qbittorrent-4.1.1/qbittorrent-4.1.1.tar.gz?r=https%3A%2F%2Fsourceforge.net%2Fprojects%2Fqbittorrent%2Ffiles%2Fqbittorrent%2Fqbittorrent-4.1.1%2Fqbittorrent-4.1.1.tar.gz%2Fdownload&ts=1528383694
```
![](https://github.com/DevComex/TechBlog/blob/master/ScreenShots/ScreenShot-2018-05-27_120126.png)

修改文件名
```
mv qbittorrent-4.1.1.tar.gz\?r\=https\:%2F%2Fsourceforge.net%2Fprojects%2Fqbittorrent%2Ffiles%2Fqbittorrent%2Fqbittorrent-4.1.1%2Fqbittorrent-4.1.1.tar.gz%2Fdownload qbittorrent-4.1.1.tar.gz
```

解压
```
tar -zxf qbittorrent-4.1.1.tar.gz
```

### 依赖项安装配置
首先需要安装依赖项
```
yum install gcc qt-devel boost boost-devel openssl-devel glibc-headers gcc-c++ -y
```

添加QT4路径到环境变量（修改/etc/profile）
```
QTDIR=/usr/lib64/qt4
PATH=$PATH:$HOME/bin:$QTDIR/bin
export PATH QTDIR
```

安装依赖项libtorrent-rasterbar
```
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

```
yum install qt5-qtbase-devel qt5-linguist -y
```
### 解压文件
```
tar -zxf qbittorrent-3.3.11.tar.gz
```
![](https://github.com/DevComex/TechBlog/blob/master/ScreenShots/ScreenShot-2018-05-27_120526.png)

### Installation:
For installation, follow the instructions from INSTALL file, but simple:

```
cd qbittorrent-3.3.11
export libtorrent_CFLAGS=/opt/libtorrent/include/libtorrent/
export libtorrent_LIBS=/opt/libtorrent/lib/
./configure --prefix=/opt/qbittorrent
make && make install
qbittorrent
```
![](https://github.com/DevComex/TechBlog/blob/master/ScreenShots/ScreenShot-2018-05-28_074739.png)

# 常见问题
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

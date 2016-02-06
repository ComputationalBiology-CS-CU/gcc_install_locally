# 1. What's this
This is an introduction to install GCC locally :sunglasses:

reference: [this](http://blog.csdn.net/yanxiangtianji/article/details/12511961) document from CSDN (Chinese version).


# 2. General procedure

This is a general introduction to the whole procedure.

1. install dependency and tools.

xxx

2. xxx

xxx





1，安装依赖库和工具
根据官方文档，如果只是为了编译安装而不是去修改gcc，那么所需要的库和工具并不是很多。
需要强调的有两点：
1）需要一个c++编译器，也就是说如果只有gcc而无g++，那么是无法完成这次编译的；
2）如果机器是64位系统同时又希望生成的编译器除了可以编译出默认的可在本机运行的64位可执行文件还可以编译出32位的可执行文件的话，需要额外安装相应的库（默认开启）。

2，配置（configure）
配置我们编译出的gcc所支持的语言，目标环境（是否为交叉编译器），依赖库路径（一定条件下可省略，下详），编译结果安装到哪里等。配置程序会根据这些信息生产Makefile文件，供下一步使用。

3，编译（make）
根据configure生成的Makefile编译出我们的gcc和相应的lib如libstdc++等。





# 3. Detailed procedure

## 3.1. Install dependency and other tools




## 3.2. Configure



## 3.3. Make



## 3.4. Afterwards




# 4. Ubuntu shell commands

Unpack gcc, and enter its folder.

```
sudo apt-get install gcc g++ make
sudo apt-get install libisl-dev libcloog-isl-dev
#若希望在64位系统下编译出32位应用程序（反之亦然），需要执行下面命令
sudo apt-get install gcc-multilib g++-multilib

sudo ./contrib/download_prerequisites
sudo mkdir build
cd build
sudo ../configure --enable-languages=c,c++
sudo make -j4sudo make install
```


# 5. Other Linux versions

The major differences are the names of different packages, and the package manager.

在升级gcc个过程中，主要区别就在于包的名字和包管理器的不同。

Ubuntu系（Debian）的包名和RedHat系（CentOS、Fedora）的在命名规则上不太一样。前缀洗好加版本号，开发版缩写为“dev”，用“-”连接架构；而后者的开发版缩写为”devel“，用”.“连接架构。
例如在安装32位的glibc的时候所使用的报名：
On Ubuntu: libc6-dev-i386.
On Red Hat distros: glibc-devel.i686
On CentOS 5.8: glibc-devel.i386
On CentOS 6.3: glibc-devel.i686

其次Ubuntu系有很多整合了的包，例如g++-multilib，build-essential等，而ReadHat系没有。




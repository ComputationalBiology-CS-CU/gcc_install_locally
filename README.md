# 1. What's this
This is an introduction to install GCC locally :sunglasses:

reference: [this](http://blog.csdn.net/yanxiangtianji/article/details/12511961) document from CSDN (Chinese version).


# 2. General procedure

This is a general introduction to the whole procedure.

1. **install dependency and tools**. You won't need too many dependency and tools if you only want to compile and install the gcc other than revising it. Here are two things you need to notice: you need to have a g++ compiler in your system to compile/install gcc; if your system is 64-bit and you want to generate a 32-bit program with your installed compiler, you need to install extra libraries (this is already the default option).
2. **configure**. Configure the languages that are supported by our installed gcc compiler, target environment (whether this is a cross compiler), the path to the dependency, where to generate the compiled gcc, etc. You will get the Makefile according to above information you provide.
3. **make**. Compile our gcc and corresponding libraries (e.g. libstdc++), with the above generated Makefile.



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




# 1. What's this
This is an introduction to install GCC locally :sunglasses:

reference: [this](http://blog.csdn.net/yanxiangtianji/article/details/12511961) document from CSDN (Chinese version).


# 2. General procedure

This is a general introduction to the whole procedure.

1. **install dependency and tools**. You won't need too many dependency and tools if you only want to compile and install the gcc other than revising it. Here are two things you need to notice: you need to have a g++ compiler in your system to compile/install gcc; if your system is 64-bit and you want to generate a 32-bit program with your installed compiler, you need to install extra libraries (this is already the default option).
2. **configure**. Configure the languages that are supported by our installed gcc compiler, target environment (whether this is a cross compiler), the path to the dependency, where to generate the compiled gcc, etc. You will get the Makefile according to above information you provide.
3. **make**. Compile our gcc and corresponding libraries (e.g. libstdc++), with the above generated Makefile.



# 3. Detailed procedure

Please refer to the official document [official document](http://gcc.gnu.org/install/) (gcc) as much as possible.

## 3.1. Install dependency and other tools

### 3.1.1. Tools

They are: g++, make, perl, unpacking tools (tar, gzip, etc.), Binutils (only under certain circumstances). Most probably you don't need to worry them too much, as they were pre-installed in most of the current Linux systems. The only thing you need to pay attention to is the c/c++ environment.

If you are sure that your system has gcc and g++, you can jump this step.

Practically, for Ubuntu, do the following:

```
apt-get install build-essential
```
which will at the same time install other necessary libraries, like glibc for development (libc-dev in Ubuntu).

Other Linux platforms usually don't have such integrated package (build-essential), so you need to install them one by one.

As you need libstdc++ and glibc (for g++ and gcc), it's recommended to use the following commend to avoid some troubles:

```
apt-get install gcc g++ make libc6-dev
```



### 3.1.2. Libraries




### 3.1.3. Practical operations


#### 3.1.3.1. Check whether they are installed already





#### 3.1.3.2. Install libraries that were not installed before




#### 3.1.3.3. Install other libraries





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




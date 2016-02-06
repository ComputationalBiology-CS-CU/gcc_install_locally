# What's this
This is an introduction to install GCC locally :sunglasses:

reference: [this](http://blog.csdn.net/yanxiangtianji/article/details/12511961) document from CSDN (Chinese version).


# General procedure


xxx

xxx


# Detailed procedure

## Install dependency and other tools




## Configure



## Make



## Afterwards




# Ubuntu shell commands

xxx

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


# Other Linux versions


xxx

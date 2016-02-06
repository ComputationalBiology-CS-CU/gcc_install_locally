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
<li class="alt"><span><span>sudo&nbsp;apt-get&nbsp;install&nbsp;gcc&nbsp;g++&nbsp;make&nbsp;&nbsp;</span></span></li><li class=""><span>sudo&nbsp;apt-get&nbsp;install&nbsp;libisl-dev&nbsp;libcloog-isl-dev&nbsp;&nbsp;</span></li><li class="alt"><span>#若希望在64位系统下编译出32位应用程序（反之亦然），需要执行下面命令&nbsp;&nbsp;</span></li><li class=""><span>sudo&nbsp;apt-get&nbsp;install&nbsp;gcc-multilib&nbsp;g++-multilib&nbsp;&nbsp;</span></li><li class="alt"><span>&nbsp;&nbsp;</span></li><li class=""><span>sudo&nbsp;./contrib/download_prerequisites&nbsp;&nbsp;</span></li><li class="alt"><span>sudo&nbsp;mkdir&nbsp;build&nbsp;&nbsp;</span></li><li class=""><span>cd&nbsp;build&nbsp;&nbsp;</span></li><li class="alt"><span>sudo&nbsp;../configure&nbsp;--enable-languages=c,c++&nbsp;&nbsp;</span></li><li class=""><span>sudo&nbsp;make&nbsp;-j4sudo&nbsp;make&nbsp;install&nbsp;&nbsp;</span></li>

```


# Other Linux versions


xxx

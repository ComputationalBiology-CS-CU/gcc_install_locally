# 1. What's this
This is an introduction to install GCC locally :sunglasses:

reference: [this](http://blog.csdn.net/yanxiangtianji/article/details/12511961) document from CSDN (Chinese version).


# 2. General procedure

This is a general introduction to the whole procedure.

1. **install dependency and tools**. You won't need too many dependency and tools if you only want to compile and install the gcc other than revising it. Here are two things you need to notice: you need to have a g++ compiler in your system to compile/install gcc; if your system is 64-bit and you want to generate a 32-bit program with your installed compiler, you need to install extra libraries (this is already the default option).
2. **configure**. Configure the languages that are supported by our installed gcc compiler, target environment (whether this is a cross compiler), the path to the dependency, where to generate the compiled gcc, etc. You will get the Makefile according to above information you provide.
3. **make**. Compile our gcc and corresponding libraries (e.g. libstdc++), with the above generated Makefile.



# 3. Detailed procedure

Please also refer to the official document [official document](http://gcc.gnu.org/install/) (gcc) as much as possible.

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

According to the official document, if you only want to install gcc other than revising it, you only need 5 third-party libraries.

They are grouped two classes: one (gmp, mpc, mpfr) can be automatically compiled when compiling gcc (downloaded the source code before and dropped them in the right places); the other (isl, cloog) needs to be installed independently.

Please prefer the version that are for development (has header files, and the library names always have "dev" or "devel").

### 3.1.3. Practical operations

#### 3.1.3.1. Check whether they are installed already


If you want to check whether library XXX has been installed, use:

```
locate libXXX
```

If you can find libXXX.so, then it's installed already.


#### 3.1.3.2. Install libraries that were not installed before

For (gmp, mpc, mpfr), run the following in the root directory of the unpacked gcc source package:

```
./contrib/download_prerequisites
```

This will download the source packages and unpack them, and create their symbolic links. According to the rulls of compiling gcc, if there are directories of gmp, mpc and mpfr, they will be automatically compiled when you compile gcc. (**Shuo**: I downloaded all the 5 packages manually and make them separately; there might be some problems if you make them automatically, though not sure).

For (isl, cloog), you can compile yourself (please refer to their official documents). If in Ubuntu, it's recommended to install them with the following command (as cloog depends on gmp and isl, and you need to configure correctly before making them):

```
apt-get intall libisl-dev libcloog-isl3
```
In specific enviroment you might need to revise the names of the libraries. You can check with "Tab" after typing "libisl" or "libcloog" (the same for things below).

#### 3.1.3.3. Install other libraries

If you want your gcc compiler to generate 32-bit programs even in 64-bit platform, you need the 32-bit running libraries, and these libraries are normally not installed in 64-bit system by default.

In Ubuntu, you can use the following simple method:

```
apt-get install gcc-multilib g++-multilib
```
In Fedora, you can use:
```
apt-get install glibc-devel.i686 libstdc++-devel.i686
```

## 3.2. Configure

### 3.2.1. Build the compiling directory

In the root directory of unpacked gcc package, create a temporary folder to save the "\*.o" files when compiling:
```
mkdir build
cd build
```

### 3.2.2. Configure

Enter the above temporary folder, call the **configure** in the root directory (of the unpacked gcc package) with other parameters. Here are some sample introductions:

```
--prefix
```
This is for setting the root folder that will save the excutable and libraries after "make install". For example, if "--prefix=/usr", then the generated gcc and g++ will be save under "/usr/bin", and generated lib will be save under "/usr/lib". If you want to substitute the original gcc and lib, then use the root directory that you find through "which gcc". By default, "--prefix" is set to "/usr/local". You can use "update-alternatives" to configure which gcc to use by default when you have several gcc.

```
--program-prefix
--program-suffix
```
Give a prefix and suffix for the generated gcc. For example, "--program-prefix=my- --program-suffix=-4.8.1" will generate "my-gcc-4.8.1".
```
--disable-multilib
```
Make the generated gcc a native compiler (the program it compiles will only be able to run in this local machine). For 64-bit system, this option is by default closed, meaning that by default the generated gcc can compile a 32-bit program or 64-bit program (with -m32). So you need to install gcc-multilib（glibc-devel.i686) first of all. For the 32-bit system, this option is opened by default, meaning gcc won't be able to compile a 64-bit program.
```
--enable-languages
```
This will specify the languages that are supported by the compiled gcc. As many people only use c and c++ from gcc, you don't have to configure other languages (I didn't). That also says, this tutorial might have some problems for compiling other languages with our installed gcc.
```
--with-gmp
--with-mpfr
--with-mpc
--with-isl
--with-cloog
--with-gmp-include
--with-gmp-lib
```
If you have installed some libraries above, and they are not in the standard lib path that will be searched, you need to set the path manually (this won't be a problem for the automatically compiled libraries). "--with-XXX=YYY" is equal to "--with-XXX-include=YYY/include" and "--with-XXX-lib=YYY/lib".


Some examples:
Let's assume the current system is 64-bit, and the current gcc is under "/usr/bin". You can use the following to have a local gcc that support c and c++ while still preserving the old gcc:
```
../configure --prefix=/usr/local --disable-multilib --enable-languages=c,c++
```

If you want to compile 32-bit program, support c and c++, and cover the old gcc, and you have installed gmp under "/usr/gmp-5.1.3/", you can use the following:
```
../configure --prefix=/usr --enable-languages=c,c++ --with-gmp=/usr/gmp-5.1.3
```

### 3.2.3. Check

Even there are some issues, the Makefile will be successfully generated by configure. However, these issues might affect the "make" process afterwards. So we need to check before making.

Open the file "config.log" that is generated with the "Makefile", and search for "error". Normally, you should only find some errors in condition information (like -Werror), or something like not supporting "-V" for the gcc when you try "gcc -V". These errors are minor. But if you can't find some files that you try to include, then it's a preventing problem.

For example, if "#include<isl/xxx.h>" has errors, that probably means you didn't install libisl-dev. If you only have a excutable libisl, you need to provide the corresponding header files by yourself. You can download its source code from official website, and pick up the header files to put in the system "include" path. Or you can specify that with "--with-isl-include=XXXX".


## 3.3. Make

Simply run:
```
sudo make -j4
```

For a better machine, you can use a larger number for the number after "-j".
If there are no problems, run:

```
sudo make install
```
This will install the compiled excutable file into the path that is configured before.

Two more things to mention:

1. gcc doesn't support "make unintall", so you should be careful if you want to cover the old gcc;
2. if you configured system path, for this step please run with root authority, otherwise it will be horrible.


## 3.4. Afterwards

If you want to have two gcc with different versions, you can definitely call the compiler with full path to it. But that seems complex.

It's recommended that you use "update-alternatives" to make the system know which gcc we mean to call when only typing "gcc" (please Google more for "update-alternatives").

For example, the newly compiled gcc is under "/usr/local/bin/gcc", and I will set a 100 priority score:
```
sudo update-alternatives --install /usr/bin/gcc gcc /usr/local/bin/gcc 100
```
Then I can use the following to check which gcc the system chooses to use (in "auto" option, the one with higher priority will be chosen):
```
sudo update-alternatives --config gcc
```
If the system doesn't automatically chooses the one we want, we can manually set their priority scores, or we can manually set the default one.


# 4. Ubuntu shell commands

Unpack gcc, and enter its folder.

```
sudo apt-get install gcc g++ make
sudo apt-get install libisl-dev libcloog-isl-dev
# if you want to compile 32-bit program in 64-bit system, then run the following:
sudo apt-get install gcc-multilib g++-multilib

sudo ./contrib/download_prerequisites
sudo mkdir build
cd build
sudo ../configure --enable-languages=c,c++
sudo make -j4sudo make install
```


# 5. Other Linux versions

The major differences are the names of different packages, and the package manager.

Packages of Ubuntu family (Debian) are named differently from those of RedHat family (CentOS, Fedora). Here are some example for 32-bit glibc:

```
On Ubuntu: libc6-dev-i386
On Red Hat distros: glibc-devel.i686
On CentOS 5.8: glibc-devel.i386
On CentOS 6.3: glibc-devel.i686
```

What's more, Ubuntu has integrated package, like g++-multilib and build-essential. While RedHat doesn't have.



# 6. Compile and run C++ program

As we installed some libraries locally that might be linked dynamically, you can add commands similar to the following in "~/.bash\_profile":

```
# this is for dynamically linking for c++ programs
export LD_LIBRARY_PATH=/ifs/scratch/c2b2/ip_lab/sy2515/HPC/shuo-gcc-4.9.1/lib:/ifs/scratch/c2b2/ip_lab/sy2515/HPC/shuo-gcc-4.9.1/lib64:/ifs/scratch/c2b2/ip_lab/sy2515/HPC/shuo-cloog-0.18.1/lib:/ifs/scratch/c2b2/ip_lab/sy2515/HPC/shuo-gmp-4.3.2/lib:/ifs/scratch/c2b2/ip_lab/sy2515/HPC/shuo-isl-0.12.2/lib:/ifs/scratch/c2b2/ip_lab/sy2515/HPC/shuo-mpfr-2.4.2/lib:/ifs/scratch/c2b2/ip_lab/sy2515/HPC/shuo-mpc-0.8.1/lib:/opt/gridengine/hpc/lib/lx-amd64

# this is for calling local gcc and local Python (Canopy, or Anaconda)
#export PATH=/ifs/scratch/c2b2/ip_lab/sy2515/HPC/shuo-gcc-4.9.1/bin:/ifs/scratch/c2b2/ip_lab/sy2515/Canopy/appdata/canopy-1.5.2.2785.rh5-x86_64/bin:$PATH
export PATH=/ifs/scratch/c2b2/ip_lab/sy2515/HPC/shuo-gcc-4.9.1/bin:/ifs/scratch/c2b2/ip_lab/sy2515/anaconda/bin:$PATH

# GPU complier and env setting
ROOT=/nfs/apps/cuda/7.5.18

export PATH=$ROOT/bin:$PATH
export LD_LIBRARY_PATH=$ROOT/lib64:$LD_LIBRARY_PATH
```

By now, you should be able to compile your c++ code (also CUDA C/C++ code) with the newly installed gcc (or nvcc in the system), and run it in the cluster. (please compile and run in computing node other than login node, as it seems there is no default gcc in login node thus lacking other necessary libraries to compile a program; also, please run GPU jobs only by submitting them to GPU nodes, as you can't login to a GPU node).


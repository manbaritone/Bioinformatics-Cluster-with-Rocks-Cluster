http://www.wikihow.com/Manually-Build-and-Install-GNU-Compiler-Collection-on-Linux-Mint

### 1. Install required packages
```
# sudo yum install binutils build-essential m4 autogen bison flex
# sudo yum install g++
```

### 2. Open up a terminal and type the following
```
# mkdir /home/"your_user_name"/gcc_archive
```

### 3. Download the following programs and place them in the gcc_archive directory
You will download all your packages you need to compile GCC to the /home/"your_user_name_"/gcc_archive directory. So change into the directory.
```
# cd /home/"your_user_name"/gcc_archive
```

### 4. While in the /home/"your_user_name"/gcc_archive directory run the following commands.
```
# wget -c ftp://ftp.gmplib.org/pub/gmp-5.1.3/gmp-5.1.3.tar.bz2
# wget -c http://www.mpfr.org/mpfr-current/mpfr-3.1.2.tar.bz2
# wget -c http://www.multiprecision.org/mpc/download/mpc-1.0.1.tar.gz
# wget -c http://ftp.gnu.org/gnu/gcc/gcc-4.8.1/gcc-4.8.1.tar.bz2
```

### 5. Install GNU GMP Multiprecision Arithmetic Library, for arbitrary precision arithmetic:
Go to ftp://ftp.gmplib.org/pub/ to download the latest version, then run these commands in the folder contains that file to extract, build and install GMP:
```
# cd /home/"your_user_name"/gcc_archive
# sudo mkdir /opt/gmp-5.1.3
# chmod a+x gmp-5.1.3.tar.bz2
# tar -jxvf gmp-5.1.3.tar.bz2
# cd gmp-5.1.3
# ./configure --prefix=/opt/gmp-5.1.3
# make && make check && sudo make install
# cd ..
```

### 6. Install GNU MPFR Library, Multiple-Precision Floating-Point computations with correct rounding
Go to http://www.mpfr.org/mpfr-current/ to download the latest version, then run these commands in the folder contains that file to extract, build and install MPFR:
```
# cd /home/"your_user_name"/gcc_archive
# sudo mkdir /opt/mpfr-3.1.2
# chmod a+x mpfr-3.1.2.tar.bz2
# tar -jxvf mpfr-3.1.2.tar.bz2
# cd mpfr-3.1.2
# ./configure --prefix=/opt/mpfr-3.1.2 --with-gmp=/opt/gmp-5.1.3
# make && make check && sudo make install

Notes: You must install GMP before installing MPFR

# cd ..
```

### 7. Install GNU MPC Library, for arithmetic using complex numbers
Go to http://www.multiprecision.org/index.php?prog=mpc&page=download to download the latest version, then run these commands in the folder contains that file to extract, build and install MPFR:
```
# cd /home/"your_user_name"/gcc_archive
# sudo mkdir /opt/mpc-1.0.1
# chmod a+x mpc-1.0.1.tar.gz
# tar -zxvf mpc-1.0.1.tar.gz
# cd mpc-1.0.1
# ./configure --prefix=/opt/mpc-1.0.1 --with-gmp=/opt/gmp-5.1.3 --with-mpfr=/opt/mpfr-3.1.2
# make && make check && sudo make install
Notes: You must install GMP and MPFR before installing MPC

# cd ..
```

### 8. Configure build options for GNU Compiler Collection (GCC)
Download the latest version of GCC from http://ftp.gnu.org/gnu/gcc/gcc-4.8.1/gcc-4.8.1.tar.bz2 . Since the GCC website did say that we should run configure command in another folder other than the source folder, we need to create another folder just for this (e.g. gcc481_build):
```
# cd /home/"your_user_name"/gcc_archive
# sudo mkdir -p /opt/gcc-4.8.1
This will create the directory which will hold the new GNU Compiler Collection (GCC)

# chmod a+x gcc-4.8.1.tar.bz2
# tar -jxvf gcc-4.8.1.tar.bz2
# mkdir gcc481_build
This will create the scratch directory to build the GNU Compiler Collection (GCC)

# cd gcc481_build
# ../gcc-4.8.1/configure --prefix=/opt/gcc-4.8.1 --with-gmp=/opt/gmp-5.1.3 --with-mpfr=/opt/mpfr-3.1.2 --with-mpc=/opt/mpc-1.0.1 --disable-multilib --enable-languages=c,c++
```

### 9. While in the gcc481_build directory, set some environment variables to prepare for the upcoming build

32-bit Linux Mint Instructions:
```
# export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/opt/gmp-5.1.2/lib:/opt/mpfr-3.1.2/lib:/opt/mpc-1.0.1/lib
# export C_INCLUDE_PATH=/usr/include/i386-linux-gnu
# export CPLUS_INCLUDE_PATH=$C_INCLUDE_PATH
# export OBJC_INCLUDE_PATH=$C_INCLUDE_PATH
# export LIBRARY_PATH=/usr/lib/i386-linux-gnu
```

64-bit Linux Mint Instructions:
```
# export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/opt/gmp-5.1.2/lib:/opt/mpfr-3.1.2/lib:/opt/mpc-1.0.1/lib
# export C_INCLUDE_PATH=/usr/include/x86_64-linux-gnu
# export CPLUS_INCLUDE_PATH=$C_INCLUDE_PATH
# export OBJC_INCLUDE_PATH=$C_INCLUDE_PATH
# export LIBRARY_PATH=/usr/lib/x86_64-linux-gnu
```

### 10. Build and install GNU Compiler Collection (GCC)
```
# make -j 4
# sudo make install
Notes: Be prepared for a long build -- it usually takes anywhere from 2 to 4 hours for a complete build, however it all depends on the speed of your processor. expect at least a 4-hour build/compile on most systems.
```

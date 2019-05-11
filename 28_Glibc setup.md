```
# unset LD_LIBRARY_PATH
# mkdir $HOME/install
# DESTDIR="$HOME/install"
# mkdir $HOME/src
# cd $HOME/src
# git clone git://sourceware.org/git/glibc.git
# mkdir -p $HOME/build/glibc
# cd $HOME/build/glibc
# $HOME/src/glibc/configure --prefix=/usr
# make -j32

# sudo make install DESTDIR=${DESTDIR}

# git clone git://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git
# cd linux
# make headers_install INSTALL_HDR_PATH="${DESTDIR}/usr"
# cp /lib64/libgcc* "${DESTDIR}/lib64/"

# strings /usr/lib64/libstdc++.so.6 | grep GLIBCXX
```

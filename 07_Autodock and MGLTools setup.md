```
# tar -xvf autodocksuite-4.2.6-x86_64Linux2.tar

# sudo mkdir /apps/autodock
# sudo mkdir /apps/mgltools
# sudo cp /pluto/admin/x86_64Linux2/* /apps/autodock

# tar -zxvf mgltools_x86_64Linux2_1.5.6.tar.gz 
# cd mgltools_x86_64Linux2_1.5.6
# sudo ./install.sh -d /apps/mgltools/

# export PATH="$PATH:/apps/autodock"
# export PATH="$PATH:/apps/mgltools/bin"
# export LD_LIBRARY_PATH="$LD_LIBRARY_PATH:/apps/mgltools/lib"
```

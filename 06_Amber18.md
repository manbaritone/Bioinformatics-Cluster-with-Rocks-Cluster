```
# export CUDA_HOME="/usr/local/cuda-9.2"

# sudo tar xvfj AmberTools19.tar.bz2
# sudo tar xvfj Amber18.tar.bz2

# sudo yum -y install tcsh make gcc gcc-gfortran gcc-c++ which flex bison patch bc libXt-devel libXext-devel perl util-linux wget bzip2 bzip2-devel zlib-devel
# sudo yum -y install scipy numpy python-matplotlib

# mv amber18 /apps

# export AMBERHOME="/apps/amber18"
# cd $AMBERHOME
```

```
# ./configure gnu (root user)
# make install -j16
```

```
# ./configure -cuda -mpi gnu
# make install -j16
```

```
# ./configure -openmp gnu
# make openmp
```

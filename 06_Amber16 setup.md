http://jswails.wikidot.com/installing-amber14-and-ambertools14

```
# export CUDA_HOME="/usr/local/cuda-8.0"

# sudo cp Amber* /apps
# sudo tar xvfj AmberTools16.tar.bz2
# sudo tar xvfj Amber16.tar.bz2

# sudo yum -y install gcc gcc-gfortran gcc-fortran gcc-c++ flex tcsh zlib-devel bzip2-devel libXt-devel libXext-devel libXdmcp-devel tkinter perl perl-ExtUtils-MakeMaker patch bison

# ln -s /usr/lib64/libgfortran.so.3.0.0 /usr/lib64/libgfortran.so 

# sudo yum -y install scipy numpy python-matplotlib
# export AMBERHOME="/apps/amber16"
# cd $AMBERHOME
```

```
# ./configure gnu (root user)
# source amber.sh 
# make install -j16
# echo "source $AMBERHOME/amber.sh" >> ~/.bashrc

# mpif90 -show
# mpicc -show
```

```
# ./configure -cuda -mpi gnu
# make install -j16
```

```
# source amber.sh
```

```
# export DO_PARALLEL="mpirun -np 2 --allow-run-as-root"
# export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda-8.0/lib:/usr/local/cuda-8.0/lib64
# export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/lib64:/usr/lib
# make test

# export DO_PARALLEL="mpirun -np 8 --allow-run-as-root"
# make test
```

```
# ./configure -openmp gnu
# make openmp
```

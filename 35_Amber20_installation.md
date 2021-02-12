System: CMake 3.12.2, CUDA 9.2, GNU7 v7.3.0, OpenMPI3 v3.1.0 with Lmod

Ref: 
https://www.hull1.com/linux/2020/08/21/complie-amber20.html
https://ambermd.org/doc12/Amber20.pdf

### Pre-installation

#Install Dependencies
```
yum -y install tcsh make \
			   gcc gcc-gfortran gcc-c++ \
			   which flex bison patch bc \
			   libXt-devel libXext-devel \
			   perl perl-ExtUtils-MakeMaker util-linux wget \
			   bzip2 bzip2-devel zlib-devel tar

yum -y install scipy numpy python-matplotlib
```

#Extract amber
```
tar xvfj AmberTools20.tar.bz2
tar xvfj Amber20.tar.bz2
```
#Create amber20 folder at destination path (e.g. /apps/amber20)
```
mkdir /apps/amber20
```

### Compile Serial CPU

#Run amber configure script
```
cd amber20_src
source amber.sh
./configure gnu
```

#Complie and install
```
cd build
cmake .. -DCMAKE_INSTALL_PREFIX=/apps/amber20 -DCOMPILER=GNU
make install -j8
```

#Test
```
cd /apps/amber20
source amber.sh
make test.serial
```

### Compile for Serial GPU

Ref: https://ambermd.org/GPUHardware.php

Amber tries to support all CUDA SDK versions up to 11.x. In the past, they have recommended CUDA 9.1 or 9.2 for the best speed of the resulting executables, but this needs to be revisited. Here are the minimum requirements for different tiers of hardware:
* Ampere (SM_80) based cards require CUDA 11.0 or later (RTX-3060, RTX-3070, RTX-3080, RTX-3090, RTX-A6000, A100).
* Turing (SM_75) based cards require CUDA 9.2 or later (RTX-2080Ti, RTX-2080, RTX-2070, Quadro RTX6000/5000/4000).
* Volta (SM_70) based cards require CUDA 9.0 or later (Titan-V, V100, Quadro GV100).
* Pascal (SM_61) based cards require CUDA 8.0 or later. (Titan-XP [aka Pascal Titan-X], GTX-1080TI / 1080 / 1070 / 1060, Quadro P6000 / P5000, P4 / P40).

* GTX-1080 cards require NVIDIA Driver version >= 367.27 for reliable numerical results.
* GTX-Titan and GTX-780 cards require NVIDIA Driver version >= 319.60 for correct numerical results.
* GTX-780Ti cards require a modified Bios from Exxact Corp to give correct numerical results.
* GTX-Titan-Black Edition cards require NVIDIA Driver version >= 337.09 or 331.79 or later for correct numerical results.

#Run amber configure script
```
module load cuda/9.2

cd /root/amber20_src
source amber.sh
./configure -cuda -noX11 gnu
```

#Complie and install
```
cd build
cmake .. -DCMAKE_INSTALL_PREFIX=/apps/amber20 -DCOMPILER=GNU -DCUDA=TRUE -DCUDA_TOOLKIT_ROOT_DIR=/usr/local/cuda-9.2
make clean
make install -j8
```

#Test
```
cd /apps/amber20
source amber.sh
make test.cuda
```

### Compile for Parallel CPU

#Run amber configure script
```
module load openmpi3

cd /root/amber20_src
source amber.sh
./configure -noX11 -openmp gnu
```

#Complie and install
```
cd build
cmake .. -DCMAKE_INSTALL_PREFIX=/apps/amber20 -DCOMPILER=GNU -DMPI=TRUE
make clean
make install -j8
```

#Test
```
cd /apps/amber20
export DO_PARALLEL='mpirun -np 2'
test -f amber.sh  && source amber.sh
export DO_PARALLEL='mpirun -np 2'
make test.parallel
```

### Compile for Parallel GPU

Ref: https://ambermd.org/GPUHardware.php

Amber tries to support all CUDA SDK versions up to 11.x. In the past, they have recommended CUDA 9.1 or 9.2 for the best speed of the resulting executables, but this needs to be revisited. Here are the minimum requirements for different tiers of hardware:
* Ampere (SM_80) based cards require CUDA 11.0 or later (RTX-3060, RTX-3070, RTX-3080, RTX-3090, RTX-A6000, A100).
* Turing (SM_75) based cards require CUDA 9.2 or later (RTX-2080Ti, RTX-2080, RTX-2070, Quadro RTX6000/5000/4000).
* Volta (SM_70) based cards require CUDA 9.0 or later (Titan-V, V100, Quadro GV100).
* Pascal (SM_61) based cards require CUDA 8.0 or later. (Titan-XP [aka Pascal Titan-X], GTX-1080TI / 1080 / 1070 / 1060, Quadro P6000 / P5000, P4 / P40).

* GTX-1080 cards require NVIDIA Driver version >= 367.27 for reliable numerical results.
* GTX-Titan and GTX-780 cards require NVIDIA Driver version >= 319.60 for correct numerical results.
* GTX-780Ti cards require a modified Bios from Exxact Corp to give correct numerical results.
* GTX-Titan-Black Edition cards require NVIDIA Driver version >= 337.09 or 331.79 or later for correct numerical results.

#Run amber configure script
```
module load cuda/9.2
module load openmpi3

cd /root/amber20_src
source amber.sh
./configure -noX11 -openmp -cuda gnu
```

#Complie and install
```
cd build
cmake .. -DCMAKE_INSTALL_PREFIX=/apps/amber20 -DCOMPILER=GNU -DMPI=TRUE -DCUDA=TRUE -DCUDA_TOOLKIT_ROOT_DIR=/usr/local/cuda-9.2
make clean
make install -j8
```

#Test
```
cd /apps/amber20
export DO_PARALLEL='mpirun -np 2'
test -f amber.sh  && source amber.sh
export DO_PARALLEL='mpirun -np 2'
make test.cuda.parallel
```
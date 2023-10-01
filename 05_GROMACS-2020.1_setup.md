```
# yum install cmake gtest
# yum install fftw fftw-devel
```

```
# tar -xvzf gromacs-2020.1.tar.gz
# cd gromacs-2020.1
# mkdir build
# cd build
# /apps/cmake-3.17.1/bin/cmake .. -DGMX_BUILD_OWN_FFTW=ON -DREGRESSIONTEST_DOWNLOAD=OFF -DGMX_MPI=ON -DGMX_OPENMP=ON -DGMX_BUILD_MDRUN_ONLY=off -DGMX_GPU=on -DGMX_SIMD=AVX2_256 -DCMAKE_INSTALL_PREFIX=/apps/gromacs-2020.1 -DCMAKE_C_COMPILER=`which gcc` -DCMAKE_CXX_COMPILER=`which g++`
# make -j16
# make check
# sudo make install
# source /apps/gromacs/bin/GMXRC
```

```
# mkdir build_non-mpi
# cd build_non-mpi
# /apps/cmake-3.17.1/bin/cmake .. -DGMX_BUILD_OWN_FFTW=ON -DREGRESSIONTEST_DOWNLOAD=OFF -DGMX_MPI=OFF -DGMX_OPENMP=OFF -DGMX_BUILD_MDRUN_ONLY=off -DGMX_GPU=on -DGMX_SIMD=AVX2_256 -DCMAKE_INSTALL_PREFIX=/apps/gromacs-2020.1 -DCMAKE_C_COMPILER=`which gcc` -DCMAKE_CXX_COMPILER=`which g++`
# make -j16
# sudo make install
# source /usr/local/gromacs/bin/GMXRC
```

```
# yum install cmake gtest
# yum install fftw fftw-devel
```

```
# tar -xvzf gromacs-5.1.4.tar.gz
# cd gromacs-5.1.4
# mkdir build
# cd build
# cmake .. -DGMX_BUILD_OWN_FFTW=ON -DREGRESSIONTEST_DOWNLOAD=OFF -DGMX_MPI=ON -DGMX_BUILD_MDRUN_ONLY=off -DGMX_USE_RDTSCP=ON -DGMX_GPU=on -DGMX_SIMD=AVX2_256 -DGMX_BUILD_UNITTESTS=OFF -DCMAKE_INSTALL_PREFIX=/apps/gromacs 
# make -j16
# make check
# sudo make install
# source /apps/gromacs/bin/GMXRC
```

```
# mkdir build_non-mpi
# cd build_non-mpi
# cmake .. -DGMX_BUILD_OWN_FFTW=ON -DREGRESSIONTEST_DOWNLOAD=OFF -DGMX_MPI=OFF -DGMX_BUILD_MDRUN_ONLY=off -DGMX_USE_RDTSCP=ON -DGMX_GPU=on -DGMX_SIMD=AVX2_256 -DGMX_BUILD_UNITTESTS=OFF -DCMAKE_INSTALL_PREFIX=/apps/gromacs 
# make -j16
# sudo make install
# source /usr/local/gromacs/bin/GMXRC
```

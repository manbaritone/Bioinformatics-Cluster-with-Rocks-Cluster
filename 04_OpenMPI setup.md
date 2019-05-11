http://www.simunano.com/2015/07/how-to-install-openmpi.html
https://www.open-mpi.org/faq/?category=building#build-rte-sge

Ver 2.0.1 

```
# tar -xzvf openmpi-2.0.1.tar.gz 
# cd openmpi-2.0.1/
# ./configure  --with-cuda="/usr/local/cuda-8.0" --with-sge="/apps/gridengine" --prefix="/apps/openmpi/"
# make -j16
# sudo make install
```

```
# export PATH="$PATH:/apps/openmpi/bin" 
# export LD_LIBRARY_PATH="$LD_LIBRARY_PATH:/apps/openmpi/lib"
```

```
ompi_info | grep gridengine  #check gridengine
```

**Add up after install software**

### Create file path.sh to folder /etc/profile.d/

```
# vi /etc/profile.d/path.sh

#!/bin/bash

export LD_LIBRARY_PATH="$LD_LIBRARY_PATH:/usr/lib64/openmpi/lib"
export LD_LIBRARY_PATH="$LD_LIBRARY_PATH:/usr/local/cuda-8.0/lib:/usr/local/cuda-8.0/lib64"
export CUDA_HOME="/usr/local/cuda-8.0"
export LD_LIBRARY_PATH="$LD_LIBRARY_PATH:/usr/local/lib64:/usr/local/lib"
export PATH="$PATH:/apps/gridengine/bin" 
export LD_LIBRARY_PATH="$LD_LIBRARY_PATH:/apps/gridengine/lib"
export PATH="$PATH:/apps/gridengine/bin/lx-amd64" 
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/apps/gridengine/lib/lx-amd64
export SGE_ROOT="/apps/gridengine"
export LD_LIBRARY_PATH="$LD_LIBRARY_PATH:/usr/lib64:/usr/lib"
export PATH="$PATH:/usr/local/bin"
export PATH="$PATH:/apps/openmpi/bin" 
export LD_LIBRARY_PATH="$LD_LIBRARY_PATH:/apps/openmpi/lib"
export MPIHOME="/apps/openmpi"
export GROMACSHOME="/apps/gromacs"
export PATH="$PATH:/apps/gromacs/bin"
export PATH="$PATH:/apps/mgltools/bin"
export LD_LIBRARY_PATH="$LD_LIBRARY_PATH:/apps/mgltools/lib"
export pkgdir="/apps/i-tasser"
export ROSETTA=/apps/rosetta/main/source/bin
export ROSETTADB=/apps/rosetta/main/database
export ANTIBODY=/apps/rosetta/tools/antibody
export PATH="$PATH:/apps/apbs/bin"
export LD_LIBRARY_PATH="$LD_LIBRARY_PATH:/apps/apbs/lib"
export PATH="$PATH:/apps/pdb2pqr" 
export LD_LIBRARY_PATH="$LD_LIBRARY_PATH:/apps/pdb2pqr"
export GMXPBSAHOME=/apps/gmxpbsatool
export PATH="$PATH:/apps/openbabel/bin"
export LD_LIBRARY_PATH="$LD_LIBRARY_PATH:/apps/openbabel/lib"
export PATH="$PATH:/apps/modeller/bin"
export LD_LIBRARY_PATH="$LD_LIBRARY_PATH:/apps/modeller/lib/x86_64-intel8"
export CCP4=/apps/ccp4
export PATH="$PATH:/apps/ccp4/bin"
export LD_LIBRARY_PATH="$LD_LIBRARY_PATH:/apps/ccp4/lib"
export PATH="$PATH:/apps/zdock"
export PATH="$PATH:/apps/zdock/deltaG"
export PATH="$PATH:/apps/zrank"
export PATH="$PATH:/apps/ncbi-blast/bin"
export BLASTDB=/apps/ncbi-blast/db
export PATH="$PATH:/apps/blast/bin"
```

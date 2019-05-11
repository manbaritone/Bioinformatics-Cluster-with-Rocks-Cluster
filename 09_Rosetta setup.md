https://www.rosettacommons.org/sites/default/files/uploads/forum/Rosetta%20Install%20Instructions.txt

```
# yum install environment-modules infinipath-psm libfabric libpsm2

# tar zxvf rosetta_bin_linux_2016.46.59086_bundle.tgz
# tar zxvf rosetta.ncaa.rotamer.libraries.tar.gz
# tar zxvf rosetta_2016.46.59086_user_guide.tgz
# sudo cp -r rosetta_bin_linux_2016.46.59086_bundle /apps
# cd /apps
# sudo mv rosetta_bin_linux_2016.46.59086_bundle ./rosetta
# cd /pluto/admin/installer/Rosetta
# sudo cp -r rosetta.ncaa.rotamer.libraries /apps/rosetta
# sudo cp -r rosetta_2016.46.59086_user_guide /apps/rosetta
# cd /apps/rosetta
# sudo mv rosetta.ncaa.rotamer.libraries ncaa.rotamer.libraries
# sudo mv rosetta_2016.46.59086_user_guide userguide
# cd main/source
# sudo ln -s /apps/openmpi/bin/mpiCC /usr/bin/mpiCC
# sudo ln -s /apps/openmpi/bin/mpicc /usr/bin/mpicc
# sudo ln -s /apps/openmpi/bin/mpic++ /usr/bin/mpic++
# sudo ln -s /apps/openmpi/bin/mpicxx /usr/bin/mpicxx
# sudo ln -s /apps/openmpi/bin/mpiexec /usr/bin/mpiexec
# sudo ln -s /apps/openmpi/bin/mpif77 /usr/bin/mpif77
# sudo ln -s /apps/openmpi/bin/mpif90 /usr/bin/mpif90
# sudo ln -s /apps/openmpi/bin/mpifort /usr/bin/mpifort
# sudo ln -s /apps/openmpi/bin/mpirun /usr/bin/mpirun
# ln -s openmpi/ /usr/lib64/
# ln -s -rf openmpi/ /usr/lib/
# mkdir /usr/include/openmpi
# ln -s /apps/openmpi/include/* /usr/include/openmpi/
# mkdir /usr/share/man/openmpi
# ln -s /apps/openmpi/share/* /usr/share/man/openmpi/
# ./scons.py -j 20 bin mode=release extras=opencl
```

```
export ROSETTA=/apps/rosetta/main/source/bin
export ROSETTADB=/apps/rosetta/main/database
export ANTIBODY=/apps/rosetta/tools/antibody
```

```
# tar -xzvf ncbi-blast-2.5.0+-x64-linux.tar.gz
# mv ncbi-blast-2.5.0+ ncbi-blast
# sudo cp -r ncbi-blast /apps
# export PATH="$PATH:/apps/ncbi-blast/bin"
# sudo mkdir /apps/ncbi-blast/db
# export BLASTDB=/apps/ncbi-blast/db
# copy nr database to /apps/ncbi-blast/db 
# tar -zxvf nr.*
```

```
# tar -xzvf blast-2.2.26-x64-linux.tar.gz
# mv blast-2.2.26 blast
# sudo cp -r blast /apps
# export PATH="$PATH:/apps/blast/bin"
# vi /etc/profile.d/.ncbirc -->
[NCBI]
data=/apps/blast/data
```

Download PyRosetta4
```
# tar -vjxf PyRosetta-<version>.tar.bz2
# mv PyRosetta4.Release.python27.linux.release pyrosetta
# cp -r pyrosetta /apps
# cd /apps/pyrosetta
# cd setup && sudo python setup.py install

# cd /apps/rosetta
# cd tools/PyRosetta.develop
# python DeployPyRosetta.py --prefix=$HOME/PyRosetta --omit-cmake
# cp $HOME/PyRosetta/BuildPyRosetta.sh /path/to/rosetta/main/source
# cd /path/to/rosetta/main/source
# ./BuildPyRosetta.sh ### This step takes ~16 hours, so do it overnight
```

Now the PyRosetta build should be in /path/to/rosetta/root/main/source/build/PyRosetta/linux/namespace/release
```
# sudo mkdir /usr/local/PyRosetta
# sudo mv /path/to/rosetta/root/main/source/build/PyRosetta/linux/namespace/release/* /usr/local/PyRosetta
```

Now there is a "database" symbolic link in /usr/local/PyRosetta that is probably broken, fortunately database just contains a bunch of text files that can be copied from the rosetta directory
```
# sudo rm /usr/local/PyRosetta/database
# sudo cp -r /path/to/rosetta/root/main/database /usr/local/PyRosetta
```

The following needs to be added to each user's .bashrc file so they can import Rosetta in Python from anywhere
```
# source /usr/local/PyRosetta/SetPyRosettaEnvironment.sh
```

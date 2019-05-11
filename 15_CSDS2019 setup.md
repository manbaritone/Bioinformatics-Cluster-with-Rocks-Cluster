```
# tar -xvf csds-2018.1-linux-x64.tar 
# ./csds-linux-x64.run 

# cd /apps/CCDC/CSD_2019/csd 
# ../bin/batch_register -current_machine -site_id XXXX -conf_code YYYYYY -email <ZZZZZZZZZZZZZZZZZZZ> -auto_accept_licence
```

### Generate license offline
https://www.ccdc.cam.ac.uk/support-and-resources/support/case/?caseid=c9c53a6b-e7e6-e611-8591-005056868fc8
```
# ssh compute-0-0
# cd /apps/CCDC/CSD_2019/csd 
# ../bin/batch_register -serial_dir /apps/CCDC/CSD_2019/csd -write_serial
# exit
```

### Online Registration
```
# cd /apps/CCDC/CSD_2019/csd
# ../bin/batch_register -serial_dir /apps/CCDC/CSD_2019/csd -write_licence -site_id XXXX -conf_code YYYYYY -email <ZZZZZZZZZZZZZZZZZZZ>
```

### For using with SGE
```
#!/bin/sh
#$ -cwd
#$ -j y

#$ -S /bin/sh

export MPI=/opt/openmpi/bin/
export LD_LIBRARY_PATH=/opt/openmpi/lib:/opt/openmpi/lib/openmpi:$LD_LIBRARY_PATH

# Define path of Gold directory.
export GOLD_DIR=“/state/partition4/home_other/nobackup/kiattawee/CCDC/GoldSuite_2018/"

# Define path of Gold license file.
export CCDC_LICENSE_FILE=/state/partition4/home_other/nobackup/kiattawee/CCDC/CSD_2018/csd/csd_licence.dat

# Add Gold lib.
export LD_LIBRARY_PATH=${GOLD_DIR}/c_linux-64/lib:${LD_LIBRARY_PATH}


###############################################

# Run Gold program.
${GOLD_DIR}/bin/gold_auto gold.conf

###############################################
```

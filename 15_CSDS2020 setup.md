```
# tar -xvf csds-2020.0-linux-x64.tar 
# ./csds-linux-x64.run 

# cd /apps/CCDC/CSD_2020/csd 
# ../bin/ccdc_activator -k XXXXXXX-XXXXXX-XXXXXX-XXXXXX-XXXXXX-XXXXXX -g -f ./master_license.dat -A
```

### Generate license offline
https://www.ccdc.cam.ac.uk/support-and-resources/support/case/?caseid=8f5d786c-682d-ea11-978f-005056977c87
```
# ssh compute-0-0
# cd /apps/CCDC/CSD_2020/csd 
# ../bin/ccdc_activator -k XXXXXXX-XXXXXX-XXXXXX-XXXXXX-XXXXXX-XXXXXX -g -f ./c0_license.dat -A
# exit
```

### Online Registration
```
# cd /apps/CCDC/CSD_2019/csd
# ../bin/ccdc_activator -k XXXXXXX-XXXXXX-XXXXXX-XXXXXX-XXXXXX-XXXXXX -a -o -f ./c0_license.dat -A
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

### Licence server setup
```
chmod a+x ccdc_licence_server-v2-linux-x64-installer.run
./ccdc_licence_server-v2-linux-x64-installer.run
```

Go to CCDCLicServer folder
```
# cd /apps/CCDC/CCDCLicServer
```

make file config.yml
```
server:
  # Port server should listen to
  port: XXXX
  # License key to activate the server
  licenseKey: XXXXXX-XXXXXX-XXXXXX-XXXXXX-XXXXXX-XXXXXX
  # Product file path
  productFilePath: ./ccdc.dat
  # Determines how long a license lease should last. The time is in seconds.
  leaseDuration: 3700
  # Allows for a time lag (in secs) between server and client machines.
  allowedClockOffset: 60
  # Blocked IP addresses
  blockedIps: []

  cryptlexHost: https://license-api.ccdc.cam.ac.uk

auth:
  # API key to access the following web API endpoints:
  # - GET /api/server/stats?apiKey=xxx
  # - GET /api/floating-licenses?apiKey=xxx
  apiKey: XXXXXXXXX
  # List of admin users who can access the dashboard
  admins:
    - username: XXXXXXXXXX
      password: XXXXXXXXXX
      # Instead of password you can also provide a SHA256 hash of the password - https://xorbin.com/tools/sha256-hash-calculator
      passwordHash:

logging:
  # Allowed log levels: "0" - Debug, "1" - Information, "2" - Warning, "3" - Errors
  logLevel: 1
  console:
    # Enable console logs
    enabled: true
    # Disable colored console logs
    noColor: true
  file:
    # Disable file logs, they will be managed by journald
    enabled: true
    # Maximum size of each log file in MBs
    maxSize: 1
    # Maximum backups to retain
    maxBackups: 10
    # Logs directory
    directory: "./logs"
```

Activate local license service
```
# ./CCDCFloatServer -a
```

Installing as a daemon on Linux
```
# ./CCDCFloatServer -i -p ./ccdc.dat -c ./config.yml --service-name ccdcfloatserver
```

Activate License for all nodes
```
cd /apps/CCDC/CSD_2002/bin
# ./ccdc_activator -A -s http://ip:port
```

Uninstalling the Licence Server service on Linux
```
# CCDCFloatServer -d
# CCDCFloatServer -u --service-name ccdcfloatserver
```

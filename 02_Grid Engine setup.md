http://gridscheduler.sourceforge.net/CompileGridEngineSource.html
http://gridscheduler.sourceforge.net/howto/GridEngineHowto.html#General Grid Engine concepts
http://biohpc.blogspot.com/2016/10/sge-installation-of-son-of-grid-engine.html
http://codingandmore.blogspot.com/2014/02/adding-head-node-of-rocks-as-compute.html

```
# yum install pam-devel openmotif lesstif openmotif-devel
# yum -y install jemalloc-devel openssl-devel ncurses-devel pam-devel libXmu-devel hwloc-devel hwloc hwloc-libs java-devel javacc ant-junit libdb-devel motif-devel csh ksh xterm db4-utils perl-XML-Simple perl-Env xorg-x11-fonts-ISO8859-1-100dpi xorg-x11-fonts-ISO8859-1-75dpi
# hostnamectl set-hostname pluto.localhost
# vi /etc/hosts
158.108.26.49  pluto.localhost pluto

# groupadd -g 490 sgeadmin
# useradd -u 495 -g 490 -r -m -s /bin/bash -c "SGE Admin" sgeadmin
# visudo >> %sgeadmin       ALL=(ALL)       NOPASSWD: ALL

# tar zxvfp sge-8.1.9.tar.gz
# cd sge-8.1.9/source/
# sh scripts/bootstrap.sh && ./aimk && ./aimk -man
# ./scripts/zerodepend

# export SGE_ROOT=/apps/gridengine && mkdir $SGE_ROOT
# echo Y | ./scripts/distinst -local -all -libs -noexit
# chown -R sgeadmin.sgeadmin /apps/gridengine
# cd $SGE_ROOT
```

```
# ./install_qmaster

press enter at the intro screen
press "y" and then specify sgeadmin as the user id
leave the install dir as /BiO/gridengine
You will now be asked about port configuration for the master, normally you would choose the default (2) which uses the /etc/services file
accept the sge_qmaster info
You will now be asked about port configuration for the master, normally you would choose the default (2) which uses the /etc/services file
accept the sge_execd info
leave the cell name as "default"
Enter an appropriate cluster name when requested
leave the spool dir as is
press "n" for no windows hosts!
press "y" (permissions are set correctly)
press "y" for all hosts in one domain
If you have Java available on your Qmaster and wish to use SGE Inspect or SDM then enable the JMX MBean server and provide the requested information - probably answer "n" at this point!
press enter to accept the directory creation notification
enter "classic" for classic spooling (berkeleydb may be more appropriate for large clusters)
press enter to accept the next notice
enter "20000-20100" as the GID range (increase this range if you have execution nodes capable of running more than 100 concurrent jobs)
accept the default spool dir or specify a different folder (for example if you wish to use a shared or local folder outside of SGE_ROOT
enter an email address that will be sent problem reports
press "n" to refuse to change the parameters you have just configured
press enter to accept the next notice
press "y" to install the startup scripts
press enter twice to confirm the following messages
press "n" for a file with a list of hosts
enter the names of your hosts who will be able to administer and submit jobs (enter alone to finish adding hosts)
skip shadow hosts for now (press "n")
choose "1" for normal configuration and agree with "y"
press enter to accept the next message and "n" to refuse to see the previous screen again and then finally enter to exit the installer
```

```
# ./install_execd --> sequencial enter
# /etc/init.d/sgemaster.pluto stop
# /etc/init.d/sgemaster.pluto start
# /etc/init.d/sgeexecd.pluto stop
# /etc/init.d/sgeexecd.pluto start
# env | grep SGE
```

```
# export PATH="$PATH:/apps/gridengine/bin/lx-amd64" 
# export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/apps/gridengine/lib/lx-amd64
```

```
# hostname
# hostname -s
# qconf -sq all.q | grep slots
# qconf -mattr queue slots '[pluto.localhost=20]' all.q
# /etc/init.d/sgemaster.pluto stop
# /etc/init.d/sgemaster.pluto start
# /etc/init.d/sgeexecd.pluto stop
# /etc/init.d/sgeexecd.pluto start
```

```
# qconf -as pluto
```

```
# qmon
Queue Control > Clone > pluto.q 
> qconf -mattr queue slots '[pluto.localhost=20]' pluto.q 
```

```
ln -s /usr/lib64/libXpm.so.4 /usr/lib64/libXpm.so
ln -s /usr/lib64/libdb-4.7.so /usr/lib64/libdb-4.4.so  
install > libdb-4.4.so
```

http://idolinux.blogspot.com/2008/09/deploying-sun-grid-engine-on-cluster.html

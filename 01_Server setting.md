### Change home directory
```
# vi /etc/default/useradd --> HOME=/pluto
```

### Add user
```
# useradd bundit
# passwd bundit
# chage -d 0 bundit
# ln -s /share/pluto/chonticha/ /pluto/
# ln -s /nasvol1 /pluto/bundit
```

### Install/remove/reinstall
```
# rpm -ivh <location file>
# rpm -Uvh <location file>
# yum install/remove/reinstall -y <package name>
```

### Change port sshd
https://www.liberiangeek.net/2014/11/change-openssh-port-centos-7/
```
# sudo semanage port -a -t ssh_port_t -p tcp 2244
# sudo yum -y install policycoreutils-python
# sudo firewall-cmd --permanent --zone=public --add-port=2244/tcp
# sudo firewall-cmd --reload
Chage in Webmin --> SSH Server --> port 2244
```

### Basic install

#### Epel repositor
```
# wget https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
# rpm -ivh epel-release-latest-7.noarch.rpm
```

#### Webmin
```
# wget http://prdownloads.sourceforge.net/webadmin/webmin-1.820-1.noarch.rpm
# yum -y install perl perl-Net-SSLeay openssl perl-IO-Tty
# rpm -U webmin-1.820-1.noarch.rpm
# firewall-cmd --permanent --zone=public --add-port=10000/tcp
```

#### Cockpit
```
# yum install cockpit
# systemctl enable --now cockpit.socket
# firewall-cmd --permanent --zone=public --add-service=cockpit
# firewall-cmd --reload
```

#### nmap
```
# yum install nmap
# yum install https://github.com/openhpc/ohpc/releases/download/v1.2.GA/ohpc-release-centos7.2-1.2-1.x86_64.rpm
# yum groupinstall "GNOME Desktop" "Graphical Administration Tools"
# yum -y update
# yum groups install "Server with GUI"
# yum install xorg-x11-server*
# yum install xorg*
# yum install boost-devel ann hdf5 
```

### Automatic Security Updates
```
# yum --security upgrade
# yum install yum-cron
# vi /etc/yum/yum-cron.conf
update_cmd = security
apply_updates = yes

# service yum-cron start 
```

### Mount point to NAS
```
# df -h
https://kb.zyxel.com/KB/searchArticle!gwsViewDetail.action?articleOid=014693&lang=EN
https://www.digitalocean.com/community/tutorials/how-to-set-up-an-nfs-mount-on-centos-6
https://www.howtoforge.com/nfs-server-and-client-on-centos-7
https://www.howtoforge.com/tutorial/setting-up-an-nfs-server-and-client-on-centos-7/
```
```
config NFS in http://158.108.26.48:4229 > DN/IP filter: 158.108.26.49/24 
# yum install nfs-utils nfs-utils-lib
# firewall-cmd --permanent --zone=public --add-service=nfs
# firewall-cmd --reload
# service rpcbind start
# systemctl start nfs
# systemctl enable nfs-server
# systemctl start nfs-server.service
# systemctl enable rpcbind
# systemctl start rpcbind
# showmount -e 158.108.26.48
# mkdir -p /nasvol1
# chmod 777 /nasvol1/
# mount 158.108.26.48:/i-data/7f067cf1/nfs/home /nasvol1
# vi /etc/fstab 
158.108.26.48:/i-data/7f067cf1/nfs/home /nasvol1    nfs    rw,sync,hard,intr   0 0
```

### Start service
```
# systemctl enable <yum-cron>
# service <yum-cron> start
```

### Reset service
```
# systemctl daemon-reload
# systemctl reset-failed
```

### Firewall
```
# firewall-cmd --permanent --zone=public --add-service=nfs
# firewall-cmd --permanent --zone=public --add-port=<port/tcp>
# firewall-cmd --reload
```

### Greeting text
```
# vi /etc/profile.d/greeting.sh

#!/bin/bash
#
echo -e "
####################################################
#
# Welcome to `hostname`
# This system is running `cat /etc/redhat-release`
# kernel is `uname -r`
#
# You are logged in as `whoami`
#
####################################################
"
```

### Change Startup to multi-user mode
```
# systemctl get-default
# systemctl set-default multi-user.target
```

### Upgrade GCC 4.9.5
```
# sudo yum install libmpc-devel mpfr-devel gmp-devel
# cd ~/Downloads
# tar xvfj gcc-4.9.5.tar.bz2
# cd gcc-4.9.5
# ./configure --disable-multilib --enable-languages=c,c++
# make -j16
# make install
```

### Web
```
# yum -y install php php-gd php-gettext php-mysql php-pdo phpmyadmin
# yum -y install php-gd php-ldap php-odbc php-pear php-xml php-xmlrpc php-mbstring php-snmp php-soap curl curl-devel
# sudo vi /etc/httpd/conf.d/phpMyAdmin.conf
Alias /phpmyadmin /usr/share/phpMyAdmin

# firewall-cmd --permanent --zone=public --add-service=http 
# firewall-cmd --permanent --zone=public --add-service=https
# firewall-cmd --reload
https://www.digitalocean.com/community/tutorials/how-to-install-and-secure-phpmyadmin-with-apache-on-a-centos-7-server
```

### Install GPU
```
# sudo rpm --install cuda-repo-<distro>-<version>.<architecture>.rpm
# sudo yum clean expire-cache
# sudo yum install cuda
# sudo yum reinstall nvidia-modprobe
# sudo chmod 666 /dev/nv*
# reboot
```

### SSL Webserver
```
# yum install mod_ssl openssl

Generate private key 
# openssl genrsa -out ca.key 2048 

Generate CSR 
# openssl req -new -key ca.key -out ca.csr

Generate Self Signed Key
# openssl x509 -req -days 365 -in ca.csr -signkey ca.key -out ca.crt

Copy the files to the correct locations
# cp ca.crt /etc/pki/tls/certs
# cp ca.key /etc/pki/tls/private/ca.key
# cp ca.csr /etc/pki/tls/private/ca.csr

# restorecon -RvF /etc/pki
# vi +/SSLCertificateFile /etc/httpd/conf.d/ssl.conf --> SSLCertificateFile /etc/pki/tls/certs/ca.crt, SSLCertificateKeyFile /etc/pki/tls/private/ca.key

# systemctl restart httpd 
# vi /etc/httpd/conf/httpd.conf

<VirtualHost *:80>
        <Directory /var/www/html>
        AllowOverride All
        </Directory>
        DocumentRoot /var/www/html
        ServerName pluto.sci.ku.ac.th
</VirtualHost>

NameVirtualHost *:443
<VirtualHost *:443>
        SSLEngine on
        SSLCertificateFile /etc/pki/tls/certs/ca.crt
        SSLCertificateKeyFile /etc/pki/tls/private/ca.key
        <Directory /var/www/html>
        AllowOverride All
        </Directory>
        DocumentRoot /var/www/html
        ServerName pluto.sci.ku.ac.th
</VirtualHost>

# systemctl restart httpd 
# firewall-cmd --permanent --zone=public --add-port=443/tcp 
# firewall-cmd --reload 
```

### Mail alert
```
http://www.tecmint.com/get-root-ssh-login-email-alerts-in-linux/
https://www.cyberciti.biz/faq/linux-unix-bsd-postfix-forward-email-to-another-account/
https://www.andreagrandi.it/2014/08/31/getting-started-with-digital-ocean-vps-configuring-dns-and-postfix-for-email-forwarding/

# systemctl restart postfix 
# systemctl enable postfix 
# firewall-cmd --add-service=smtp --permanent 
# firewall-cmd --reload 
http://www.krizna.com/centos/setup-mail-server-centos-7/
http://www.tecmint.com/setup-postfix-mail-server-and-dovecot-with-mariadb-in-centos/
https://www.howtoforge.com/tutorial/configure-postfix-to-use-gmail-as-a-mail-relay/
https://jaredbusch.com/2014/12/28/setup-postfix-on-centos-7-to-relay-mail-to-an-internal-exchange-server/
```

### Automount USB
```
# yum install pmount

1. add a file automount.rules in /etc/udev/rules.d
2. add the following lines to automount.rules

automount.rules

# automounting usb flash drives
# umask is used to allow every user to write on the stick
# we use --sync in order to enable physical removing of mounted memory sticks -- this is OK for fat-based sticks
# I don't automount sda since in my system this is the internal hard drive
# depending on your hardware config, usb sticks might be other devices than sdb*
ACTION=="add",KERNEL=="sdb*", RUN+="/usr/bin/pmount --sync --umask 000 %k"
ACTION=="remove", KERNEL=="sdb*", RUN+="/usr/bin/pumount %k"
ACTION=="add",KERNEL=="sdc*", RUN+="/usr/bin/pmount --sync --umask 000 %k"
ACTION=="remove", KERNEL=="sdc*", RUN+="/usr/bin/pumount %k"

3. udevadm control --reload-rules
```

https://www.digitalocean.com/community/tutorials/how-to-install-bacula-server-on-centos-7

```
# sudo yum install -y bacula-director bacula-storage bacula-console bacula-client mariadb-server
# sudo mysql_secure_installation
# sudo systemctl start mariadb
# /usr/libexec/bacula/grant_mysql_privileges -u root -p
# /usr/libexec/bacula/create_mysql_database -u root -p
# /usr/libexec/bacula/make_mysql_tables -u bacula -p
# mysql -u root -p
# MariaDB [(none)]> UPDATE mysql.user SET Password=PASSWORD('XXXXXXXXXX') WHERE User='bacula';
# MariaDB [(none)]> FLUSH PRIVILEGES;
# MariaDB [(none)]> exit
# sudo systemctl enable mariadb
# sudo alternatives --config libbaccats.so --> 1
# sudo vi /etc/bacula/bacula-dir.conf
--> Add Director DirAddress: DirAddress = 127.0.0.1
--> Rename BackupClient1 job: BackupClient1 --> BackupLocalFiles
--> Rename RestoreFiles job: RestoreFiles --> RestoreLocalFiles
--> Update "Full Set" FileSet: compression = GZIP, File = /
--> Update Catalog dbpassword: dbpassword = "XXXXXXXXXXX"
--> Update Pool: Label Format = Local-
# sudo bacula-dir -tc /etc/bacula/bacula-dir.conf
```

```
# sudo systemctl start bacula-dir
# sudo systemctl start bacula-sd
# sudo systemctl start bacula-fd
# sudo systemctl enable bacula-dir
# sudo systemctl enable bacula-sd
# sudo systemctl enable bacula-fd
```

### Manage Bacula With Webmin
https://www.unixmen.com/install-and-configure-bacula-server-in-centos-6-4-rhel-6-4/
```
# firewall-cmd --permanent --zone=public --add-port=9101/tcp
# firewall-cmd --permanent --zone=public --add-port=9102/tcp
# firewall-cmd --permanent --zone=public --add-port=9103/tcp
# firewall-cmd --reload
```

### Webmin
unused modules
Bacula Backup System
Module Configuration --> Select the database i.e “MySQL”, Password: XXXXXXXXXXXX

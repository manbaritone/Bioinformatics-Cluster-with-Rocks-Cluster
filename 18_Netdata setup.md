https://github.com/firehol/netdata/wiki/Installation

https://www.vultr.com/docs/installing-netdata-on-centos-7

http://www.tecmint.com/netdata-real-time-linux-performance-network-monitoring-tool

### netdata Installation on Linux Systems

```
# sudo pacman -S netdata         [Install Netdata on Arch Linux]
# sudo emerge --ask netdata      [Install Netdata on Gentoo Linux]
# sudo eopkg install netdata     [Install Netdata on Solus Linux]
# sudo apk add netdata           [Install Netdata on Alpine Linux]
```

```
# bash <(curl -Ss https://my-netdata.io/kickstart.sh            [On 32-bit]
# bash <(curl -Ss https://my-netdata.io/kickstart-static64.sh)  [On 64-bit]
```

The above script will:

- discover the distribution and installs the needed software packages for building netdata (will ask for confirmation).\
- downloads the latest netdata source tree to /usr/src/netdata.git.\
- installs netdata by executing ./netdata-installer.sh from the source tree.\
- installs netdata-updater.sh to cron.daily, so your netdata will be updated daily (you will receive a alert from cron only if the update fails).

Note: The kickstart.sh script progress all its parameters to netdata-installer.sh, so you can define more parameters to modify the installation source, enable/disable plugins, etc.

### On Centos / Redhat / Fedora
```
# yum install zlib-devel gcc make git autoconf autogen automake pkgconfig
```
Next, clone the netdata repository from git and run netdata installer script to build it.
```
# git clone https://github.com/firehol/netdata.git --depth=1
# cd netdata
# ./netdata-installer.sh
```

Note: The netdata-installer.sh script will build netdata and install it on your Linux system.\
Once the netdata installer finishes, the file /etc/netdata/netdata.conf will be created in your system.\
Now it’s time to start netdata by executing the following command from the terminal.

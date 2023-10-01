
### Remove old driver

```
$ nvidia-uninstall
$ yum remove nvidia*
$ reboot now
```

### Set Grub nouveau.modeset=0

```
$ vi /etc/default/grub 
add nouveau.modeset=0 in GRUB_CMDLINE_LINUX 

$ grub2-mkconfig -o /boot/efi/EFI/centos/grub.cfg
$ systemctl isolate multi-user.target
$ systemctl set-default multi-user.target
$ reboot now
```

### Prepare Installation

```
$ yum install kernel-* epel-release libglvnd-devel gcc
$ reboot now
```

### Disabling Nouveau

```
$ vi /etc/modprobe.d/blacklist-nouveau.conf 
blacklist nouveau
options nouveau modeset=0

$ dracut --force
```

### Install Driver & Cuda Toolkits

```
$ wget http://developer.download.nvidia.com/compute/cuda/10.2/Prod/local_installers/cuda_10.2.89_440.33.01_linux.run
$ chmod +x cuda_10.2.89_440.33.01_linux.run
$ ./cuda_10.2.89_440.33.01_linux.run
$ reboot now
```

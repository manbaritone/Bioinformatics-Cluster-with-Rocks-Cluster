Follow up with http://linoxide.com/how-tos/centos-7-step-by-step-screenshots/
https://wiki.centos.org/HowTos/InstallFromUSBkey

1. Download CentOS 7 Installation http://mirror1.ku.ac.th/centos
2. Bootable usb disk in mac os
- Check mount point of usb disk using command "diskutil list"
- Open Disk Utility Program format usb in Fat type
- Unmount usb disk
- Create disk using command "dd if=/path/of/iso/file of=/dev/disk2"
- Waiting for disk creation about 1 hr - 2 hr 
3. Restart your computer and set up your BIOS to UEFI support
4. Restart again and boot up with usb drive that included with CentOS installation files
5. Select Language and Keyboard and Time
6. Setup Network & Hostname
7. Select version of CentOS 7 that would like to install in your computer, for pluto server choose "Server with GUI" version and choose module softwares in the right panel with all softwares except  E-mail server, KDE, DNS Name Server, Print server, Visualization Hypervisor, Smart Card Authentication
8. Setup Installation Destination 
- Choose disk to installation
- Select partitioning with "I will configure partitioning" menu
- Select standard partition
      - /boot --> 500mb (Fix capacity)
      - /boot/efi --> 200mb (Fix capacity)
      - / (root) --> Non fix capacity (Up to you)
      - /home --> Non fix capacity (Up to you)
      - /var --> Non fix capacity (Up to you) but less than /home and / (root)
      - /swap  --> Normally, 2 folds of RAM or 1 fold of RAM 

* For pluto server, I would like change /home to /pluto for security when open to public

9. Begin Installation with setup root password and create a user account

* For pluto server, create a user account menu, I would like create username with "admin" and change destination home directory to /pluto/admin

10. CentOS 7 will be install about 15-20 min depend on capability of your system 

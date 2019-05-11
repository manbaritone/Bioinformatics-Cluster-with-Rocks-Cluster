![Alt text](http://i1-linux.softpedia-static.com/screenshots/Rocks-Cluster_1.png)

## Pre-setup and Installtion Rocks with USB

### Frontend Node (Master node)

1) Cluster that will be install, must setup BIOS by enable PXE or Network Booting and setup usb boot in first order
2) Download the lastest version of Rocks from http://www.rocksclusters.org, download jumbo (DVD) version
3) Download Rufus from https://rufus.akeo.ie/ and setup with usb on Windows, using ISO image file that downloaded from Rocks website
4) When usb bootable is finished, then adjust parameter files in usb by following (credit: https://lists.sdsc.edu/pipermail/npaci-rocks-discussion/2016-March/068852.html and modify with slightly):

    4.1 Go to /isolinux folder open "isolinux.cfg" with text editor, change "ks=cdrom:/ks.cfg" to "ks=hd:sda1:/ks.cfg" and add and add "repo=hd:sda1:/kernel/6.2/x86_64" at the back of the line
    4.2 Modify "ks.cfg" file by remove the line "url --url http://127.0.0.1/mnt/cdrom/kernel/6.2/x86_64"
    4.3 Create a file on the USB drive called "rocks.conf" with contents
 
            var.trackers = 127.0.0.1
            var.pkgservers = 127.0.0.1
    
5) Now you can boot with your USB drive, restart your computer and Rocks installtion will be start from usb
6) User will have a manual step to perform. When you get to the point where the installation says "http://127.0.0.1/ .... not responding," do the following
        
    get to the shell prompt: <ctrl-alt-F2>
        
    1. mount your usb drive under /mnt/cdrom      
          ```# mount /dev/sda1 /mnt/cdrom```
    2. copy /mnt/cdrom/rocks.conf /tmp
          ```# cp /mnt/cdrom/rocks.conf /tmp```
    3. start lighttpd
          ```# /lighttpd/sbin/lighttpd -f /lighttpd/conf/lighttpd.conf```
 
    go back to the graphical interface and ask it to reload the page (alt-F6). Pick the rolls you want from local CD/DVD. They should all be there.
 
7) When get disk partition, select "manual partitioning", your flash drive looks like a disk drive, you want to make sure that you install on the correct drive. Please study a manual setup from http://central6.rocksclusters.org/roll-documentation/base/6.2/install-frontend.html

### Compute node

1) Compute nodes must setup BIOS by enable PXE or Network Booting
2) In Frontend node run terminal and enter "insert-ethers" 
3) Start up compute node with Network Booting (don't plug in USB at the compute nodes)
4) Compute node will be install automatically. You can study manual from http://central6.rocksclusters.org/roll-documentation/base/6.2/install-compute-nodes.html

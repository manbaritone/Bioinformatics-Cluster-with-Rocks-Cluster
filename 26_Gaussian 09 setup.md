http://orastuf.blogspot.com/2013/12/gaussian09-installation-under-centos.html

```
# tar -zxvf Desktop/XXX.tgz
# cp -r g09 /app/g09
# chgrp -Rv g09 g09
# cd g09
# ./bsd/install

# g09root=/apps/g09
# GAUSS_SCRDIR=/scratch/$USER
# export g09root GAUSS_SCRDIR
# . $g09root/g09/bsd/g09.profile
```

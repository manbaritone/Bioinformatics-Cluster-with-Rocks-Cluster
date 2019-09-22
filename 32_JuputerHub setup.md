https://medium.com/@dzeyelid/check-easy-install-jupyterhub-and-jupyterlab-includes-trouble-shooting-of-installing-365b39603537


### Install anaconda3
```
# curl -O https://repo.continuum.io/archive/Anaconda3-5.1.0-Linux-x86_64.sh
# bash Anaconda3-5.1.0-Linux-x86_64.sh 
```

### Install packages that are required by jupyterlab/hub-extension
```
# sudo yum groupinstall -y "Development tools"
# sudo yum install -y cairo-devel libjpeg-turbo-devel
```

### Install jupyterhub, jupyterlab and extension
```
# cd ~
# source ~/anaconda3/bin/activate
# conda install -y -c conda-forge jupyterhub
# conda install -y -c conda-forge jupyterlab
# jupyter labextension install -y @jupyterlab/hub-extension
# /apps/anaconda3/bin/pip install git+https://github.com/jupyter/sudospawner
```

### Run jupyterhub (Note: this is just an example, please configure according to your situation.)
```
# vi /lib/systemd/system/jupyterhub.service

[Unit]
Description=Jupyterhub
After=syslog.target network.target

[Service]
User=root
Environment="PATH=/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/apps/anaconda3/bin"
ExecStart=/apps/anaconda3/bin/python /apps/anaconda3/bin/jupyterhub --Spawner.cmd="['jupyter-labhub']" --no-ssl --JupyterHub.spawner_class=sudospawner.SudoSpawner -f /apps/anaconda3/etc/jupyter/jupyterhub_config.py
WorkingDirectory=/apps/anaconda3/etc/jupyter/

WorkingDirectory=/apps/anaconda3/etc/jupyter/

[Install]
WantedBy=multi-user.target
```

```
# systemctl start jupyterhub
# systemctl enable jupyterhub
```

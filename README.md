mydevstack
==========
scripts to create my own devstack environment
uses Vagrant to deploy a VM.

Deploy VM
---------
```
$ vagrant up
$ vagrant ssh
> sudo reboot   ### reboot required because of apt-get upgrade
```

Setup devstack
--------------
```
$ vagrant ssh
> cd devstack
> ./stack.sh
```

VM spec
-------
* CPU: 2core
* MEM: 4096MB
* HDD: 40GB
* NIC:
-- eth0 - NAT
-- eth1 - Host only (vboxnet2) ... DHCP enabled 192.168.33.0/24

Install OS
----------
* Ubuntu 14.04LTS server [boxfile](https://cloud-images.ubuntu.com/vagrant/trusty/current/trusty-server-cloudimg-amd64-vagrant-disk1.box)

mydevstack
==========
scripts to create my own devstack environment

Create VM
---------
* CPU: 1core
* MEM: 2048MB
* HDD: 16GB
* NIC:
-- eth0 - NAT
-- eth1 - Host only (vboxnet0) ... DHCP enabled 192.168.56.101-200

Install OS
----------
* Ubuntu 14.04.1LTS server

-- OpenSSH enabled

Setup network
-------------
* eth0: dhcp
* eth1: 192.168.56.10/24 (static)

-- Use the interfaces file on github

Setup OS
--------
```
$ apt-get update
$ apt-get upgrade
$ apt-get install git
```

Git cloning
-----------
```
$ git clone -b stable/juno git://github.com/openstack-dev/devstack.git
$ git clone git://github.com/tetsuyasodo/mydevstack
$ cd devstack
$ ln -s ../mydevstack/localrc .
```

Run devstack
------------
```
$ ./stack.sh
```

Stop devstack and restart
-------------------------
```
$ ./unstack.sh
$ OFFLINE=True ./stack.sh
```

or...

```
$ sudo losetup -f /opt/stack/data/stack-volumes-backing-file
$ cd ./devstack && ./rejoin-stack.sh
```

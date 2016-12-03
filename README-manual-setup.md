How to manually setup a VM
==========================
steps to create my own devstack environment.
uses VirtualBox to deploy a VM manually.

Create VM
---------
* CPU: 1core
* MEM: 2048MB
* HDD: 16GB
* NIC:
-- eth0 - NAT
-- eth1 - Host only (vboxnet0) ... DHCP enabled 192.168.33.0/24

Install OS
----------
* Ubuntu 14.04.1LTS server

-- OpenSSH enabled

Setup network
-------------
* eth0: dhcp
* eth1: 192.168.33.10/24 (static)

-- Use the interfaces file on github

Setup OS
--------
```
$ apt-get update
$ apt-get upgrade
$ apt-get install git
$ git config --global url."https://".insteadOf git://
$ export http_proxy=http://xxx:8080
$ export https_proxy=http://xxx:8080
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

Other components
----------------
* sahara
```
# Enable Sahara
SAHARA_BRANCH=${SAHARA_BRANCH:-stable/juno}
ENABLED_SERVICES+=,sahara
#enable_service sahara
```

and append the following line in ~/devstack/files/apts/horizon
```
apache2 # NOPRIME
gettext ### for sahara
libapache2-mod-wsgi # NOPRIME
```

* LBaaS
```
enable_service q-lbaas
```

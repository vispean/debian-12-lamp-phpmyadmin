# Debian 12 LAMP

Provisioning of a debian 12 machine with a LAMP stack and possibly phpMyAdmin and/or a local python installation

## Build virtual machine in virtualbox

- open console/terminal in this directory
- issue the following command: `vagrant up`
- this should download the corresponding vagrant box and add it to `~/.vagrant.d/boxes`
- load the box into virtualbox
- start the new virtual machine in virtualbox
- replace ssh keys
- provision a few scripts (installing a web server, a database, php and phpMyAdmin)

## Options within Vagrantfile

- `config.vm.box`: choose three other vagrant boxes
- `vb.gui`: start the virtual machine with a window while provisioning
- `vb.memory`: set desired memory size of the virtual machine (default is 2048 MB)
- `config.vm.provision`: provision an additional script for smaller conveniences (requires a desktop environment)

## Manual provisioning

- if the provisioning with virtualbox should not work, there is a shell script in scripts that can be run on the guest machine: setup.sh
- in the Vagrantfile comment all `config.vm.provision` options out
- vagrant up
- in the virtualbox GUI mount the folder `manual_provisioning` onto `/mnt` (see screenshots --> virtualbox_01 - virtualbox_03 [hint: in screenshot virtualbox_03 the folder to be mounted is named `Übung_01` and not `manual_provisioning`])
- issue the following commands:
- `cd /mnt`
- `sh setup.sh`
- power off virtual machine (make sure the virtual machine is not running): `history -c && sudo shutdown -h now`
- AFTER manual provisioning (otherwise nothing will be installed during provisioning) switch in virtualbox the first network adapter of the virtual machine from nat to hostonly (see screenshots --> virtualbox_04 - virtualbox_05)
- start virtual machine
- login directly in to the virtual machine (vagrant ssh doesn't work anymore)

## Windows remarks

- if the host is a windows machine, make sure that you installed virtualbox with admin rights (run the installation exe as administrator; is required for setting up network adapters), otherwise private networks / host-only adapters won't work, aka this provisioning

## Sakila

- the data used for populating the sakila database is taken from mysql: https://dev.mysql.com/doc/sakila/en/
- many thanks to Mike Hillyer and all the other contributors

## Connect from host to guest
- to get the ip address of the guest machine run on the guest machine the following command: `ip addr show` (see screenshots --> virtualmachine_01)
- open the browser on the host machine
- enter http://`<insert guest ip address>`/phpMyAdmin (for example: http://192.168.56.10/phpMyAdmin)

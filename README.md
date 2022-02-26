libvirt-host, an Ansible role
====================================

This role sets up a libvirt environment on a fresh RHEL 9 host. 

The role creates these resources. 
I haven't got around to writing something to delete them and return to a shiny new state.

* libvirt volume storage pool _images_. This is the default that would get created anyway. ISO files and disk images go here.
* libvirt network _public0_. Virtual machines that serve the network go here. I don't touch the default NAT network _default_.
* libvirt networks _private0_ and _private1_. These are for experiments with administering those hard-to-reach places.

I wrote this role to help me decipher https://libvirt.org/daemons.html.
Try the libvirt-guest role after this (https://github.com/nickhardiman/libvirt-guest).

Requirements
------------

A physical machine running RHEL 9. 

To run the "myfirstvm" test playbook below, you need this 
ready-made KVM file _/var/lib/libvirt/images/rhel-8.2-x86_64-kvm.qcow2_. Download this from https://access.redhat.com/downloads/. Sign up for free at https://developers.redhat.com/ to get access.


Role Variables
--------------

It's early days, so everything is hard-coded. 

Dependencies
------------

community.libvirt

Example
-------

Install everything.

```
sudo dnf install ansible-core
sudo ansible-galaxy collection install community.libvirt --collections-path /usr/share/ansible/collections/ansible_collections
mkdir -p ~/ansible/roles
cd ~/ansible/roles
git clone https://github.com/nickhardiman/virtualization-host.git
sudo ansible-playbook virtualization-host/tests/test.yml
```

Create and destroy a VM. 

```
sudo ansible-playbook virtualization-host/tests/vm-myfirstvm.yml
```

License
-------

BSD

Author Information
------------------

Nick Hardiman


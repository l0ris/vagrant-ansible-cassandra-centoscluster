# Vagrant For Cassandra CentOS 7 virtual clusters

To  create a Cassandra Cluster via Vagrant + Ansible. 

## Prerequisites


Install  the following packages in yur base machine,
Vagrant
VirtualBox 
Ansible 


Also, make sure you are running Ansible v1.7.2 or higher with `ansible --version`.

For more information, checkout the installation pages of [Vagrant](https://docs.vagrantup.com/v2/installation/), [VirtualBox](https://www.virtualbox.org/wiki/Downloads) and [Ansible](http://docs.ansible.com/intro_installation.html).


## Usage


In terminals, run the following command,

```
vagrant up 
```

to check the statu 

```
vagrant status
```
to ssh to the virtual machine,

```
vagrant ssh cassandra-node-1
```

Running Demo :

https://youtu.be/t9ypo-XYBvw


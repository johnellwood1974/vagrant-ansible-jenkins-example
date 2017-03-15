# vagrant-ansible-jenkins-example

## Pre-reqs
* 2 CPU cores, 1 for each VM
* RAM

## Installation on Ubuntu
1. sudo apt-get install vagrant ansible virtualbox
2. git clone https://github.com/johnellwood1974/vagrant-ansible-jenkins-example
3. cd vagrant-ansible-jenkins-example
4. ansible-galaxy install geerlingguy.jenkins -p .
5. ansible-galaxy install geerlinguy.apache -p .
6. vagrant up

Thanks to geerlingguy for the excellent Ansible roles which do all the heavy lifting.

## Server access
* vagrant ssh web1
* vagrant ssh jenkins
* http://192.168.10.2
* http://192.168.100.2 (admin/jenkins)

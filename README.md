# vagrant-ansible-jenkins-example

## Pre-reqs
* 2 CPU cores, 1 for each VM
* 1 GB RAM, 512MB for each VM

## Installation on Ubuntu
1. sudo apt-get install vagrant ansible virtualbox python-jenkins
2. git clone https://github.com/johnellwood1974/vagrant-ansible-jenkins-example
3. cd vagrant-ansible-jenkins-example
4. ansible-galaxy install geerlingguy.jenkins -p .
5. ansible-galaxy install geerlinguy.apache -p .
6. vagrant up

Thanks to geerlingguy for the excellent Ansible roles which do all the heavy lifting.

## VM access
* vagrant ssh web1
* vagrant ssh jenkins
* http://localhost:8012/website
* http://localhost:8080 (admin/admin)

## CD pipeline
* http://localhost:8080/ ....
* Check jobs are building every minute without errors

On your local box:
* cd website_content
* update index.html
git add index.html
git commit -m "Updated index.html"

Wait 1 minute
Check jenkins job builds and updates content
Check website has updated: http://localhost:8012/website

## Cleaning up
* vagrant destroy -f

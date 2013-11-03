capistrano-glusterfs
====================

A Capistrano 3 recipie for deploying GlusterFS.

You can install the latest master version of GlusterFS in parallel.


## Glossary

* Targetted node means a node on which you are going to install GlusterFS.
* Executing node means a node where you are going to execute capistrano-glusterfs.


## Requirements

### Targetted node(s)

* Red Hat Enterprise Linux 6.4 x86 64bit (or another conpatible Linux distribution).
* Sshd is running and publickey authentication is enabled between the users on the executing node and the targetted nodes. (Some cloud services are supported as default.)
* The user on each targetted node is enable to run sudo without a password. (Some cloud services are supported as default.)

#### Pre-execution procedure

`````bash
# user="deploy"
# useradd -g root -G wheel $user
# passwd $user
# visudo
# egrep '^%wheel.*NOPASSWD' /etc/sudoers
# chmod 775 /usr/local/src
# yum install -y openssh-clients
# su - $user
$ echo 'export PATH=$PATH:/bin:/usr/bin' >> ~/.bashrc
$ source ~/.bashrc
$ mkdir -p ~/.ssh -m 700
$ mv id_rsa authorized_keys ~/.ssh/
$ chmod 600 ~/.ssh/{authorized_keys,id_rsa}
`````

### Executing node

* Git
* Ruby >= 1.9.3


## Installation on the executing node

`````bash
$ git clone https://github.com/keithseahus/capistrano-glusterfs.git
$ cd capistrano-glusterfs
$ gem install bundler
$ bundle install
$ bundle exec cap install
$ cp ./config/deploy.rb.example ./config/deploy.rb
$ cp ./config/deploy/staging.rb.example ./config/deploy/staging.rb
`````

## Configuration on the executing node

`````bash
$ vi ./config/deploy/staging.rb
`````


## Usage on the executing node

### Show usage

`````bash
$ bundle exec cap -vT | grep -i glusterfs
`````

### Start deployment with the staging configuration

`````bash
$ bundle exec cap staging deploy
`````


## Support

Pull requiest is welcomed.

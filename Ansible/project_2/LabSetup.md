# Install Vagrant
https://www.vagrantup.com/docs/installation

# Install Oracle Virtualbox

https://www.vagrantup.com/docs/providers/virtualbox

# Lab
```
vagrant up
vagrant ssh control
```

### Copy over hosts file
```
sudo cp /vagrant/hosts /etc/hosts
```

## Install Ansible on control station
```
sudo apt-get install ansible -y
```

## Make hosts SSH accessible
```
ssh-keygen
ssh-copy-id vm1 && ssh-copy-id vm2 && ssh-copy-id vm3
```

### Test ansible
```
ansible nodes -i myhosts -m command -a hostname
```

### Install Python 
```
ansible nodes -i myhosts -m command -a 'sudo apt-get -y install python-simplejson'
```
https://github.com/devopsjourney1/devops-project2021/tree/master/solution/1.LabSetup
### Run the playbook to install docker
```
ansible-playbook -i myhosts -K playbook1.yml
```
### Vagrant-cheat-sheet
https://gist.github.com/devopsjourney1/7a5f21fddef564eb8c68dd7901d0f6be

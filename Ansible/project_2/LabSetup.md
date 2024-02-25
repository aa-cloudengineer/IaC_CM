# Step: 1 
### Install Vagrant
https://www.vagrantup.com/docs/installation

# Step: 2 
### Install Oracle Virtualbox
https://www.vagrantup.com/docs/providers/virtualbox

# Step: 3
- Create Vagrantfile which will provision the desired environment (controller VM and 3 target VMs)
- Create myhosts file for the inventory
- Create playbook1.yml to configure the target servers

### Connect to the controler 
```
vagrant up
vagrant ssh control
```

### Copy over hosts file
```
sudo cp /vagrant/myhosts /etc/myhosts
```

### Install Ansible on control station
```
sudo apt-get install ansible -y
```

### Make hosts SSH accessible
```
ssh-keygen
ssh-copy-id vm1 && ssh-copy-id vm2 && ssh-copy-id vm3
```

### Test ansible
```
ansible Target-Servers -i myhosts -m command -a hostname
```

### Install Python 
```
ansible Target-Servers -i myhosts -m command -a 'sudo apt-get -y install python-simplejson'
```
### Run the playbook to install docker
```
ansible-playbook -i myhosts -K playbook1.yml
```
### Vagrant-cheat-sheet
https://gist.github.com/devopsjourney1/7a5f21fddef564eb8c68dd7901d0f6be

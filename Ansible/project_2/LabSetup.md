# Step: 1 - Environment Setup
### Install Vagrant
https://www.vagrantup.com/docs/installation

### Install Oracle Virtualbox
https://www.vagrantup.com/docs/providers/virtualbox

- Create Vagrantfile which will provision the desired environment (controller VM and 3 target VMs)
- Create myhosts file for the inventory
- Create playbook1.yml to configure the target servers

# Step 2 Install Ansible on control station
```
sudo apt-get install ansible -y

Vagrant.configure("2") do |config|
                    servers=[
                        {
                          :hostname => "control",
                          :box => "bento/ubuntu-18.04",
                          :ip => "172.16.1.50",
                          :ssh_port => '2200'
                        },
                        {
                          :hostname => "vm1",
                          :box => "bento/ubuntu-18.04",
                          :ip => "172.16.1.51",
                          :ssh_port => '2201'
                        },
                        {
                          :hostname => "vm2",
                          :box => "bento/ubuntu-18.04",
                          :ip => "172.16.1.52",
                          :ssh_port => '2202'
                        },
                        {
                          :hostname => "vm3",
                          :box => "bento/ubuntu-18.04",
                          :ip => "172.16.1.53",
                          :ssh_port => '2202'
                        }        
                      ]
                
                    servers.each do |machine|
                        config.vm.define machine[:hostname] do |node|
                            node.vm.box = machine[:box]
                            node.vm.hostname = machine[:hostname]
                            node.vm.network :private_network, ip: machine[:ip]
                            node.vm.network "forwarded_port", guest: 22, host: machine[:ssh_port], id: "ssh"
                            node.vm.provider :virtualbox do |vb|
                                vb.customize ["modifyvm", :id, "--memory", 512]
                                vb.customize ["modifyvm", :id, "--cpus", 1]
                            end
                        end
                    end
                end
```
# Step 3 - Connect to the controler 
```
vagrant up
vagrant ssh control
```

### Copy over hosts file
```
sudo cp /vagrant/myhosts /etc/myhosts
```

### Make hosts SSH accessible
```
ping v1, v2 and v3
```

### Make hosts SSH accessible - Password-less authontication
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

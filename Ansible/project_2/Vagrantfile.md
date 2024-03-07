 provider "aws" {
            access_key = "your-access-key"
            secret_key = "your-secret-key"
            region     = "us-west-2"
          }
          
          resource "aws_instance" "example" {
            ami           = "ami-0c55b159cbfafe1f0"
            instance_type = "t2.micro"
            key_name      = "your-key-pair-name"
          
            tags = {
              Name = "example-instance"
            }
          }



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

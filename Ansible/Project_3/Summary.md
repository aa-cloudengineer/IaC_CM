# Ansible Hands-On | Step by Step for Beginners
## Pre-requests 
- We will need Linux machines for this DEMO. You can use any Linux machines or setup using any cloud platforms like AWS
- In this Demo we going to use Vagrant to create Linux Virtual Machines
- steps will remain same for both methods (locally (Vagrant) or clould platform)

 ## Part A - Ansible Controller Machine Setup
- Step 1 - Install VirtualBox and Vagrant on your local machine.
- Step 2 - Open a terminal and navigate to the directory where you want to set up
  your Ansible project.
- Step 3 - Create a new directory for your Ansible controller VM by running the
  command mkdir ansible-controller
- Step 4 - Navigate to the directory and create a new file called Vagrantfile by
  running the command vagrant init centos/7
- Step 5 - Edit the Vagrantfile and add the following lines to the end of the file to
  provision Ansible on the VM

 Edit Vagrantfile with these lines below
 
    config.vm.provision "shell", inline: <<-SHELL
    sudo yum install epel-release -y
    sudo yum install ansible -y
    SHELL
    
 Vagrantfile for creating VM for Ansible Controller

    Vagrant.configure("2") do |config|
    config.vm.define "ansible-controller" do |controller|
    controller.vm.hostname = "controller"
    end
    config.vm.box = "centos/7"
    config.vm.provision "shell", inline: <<-SHELL
    sudo yum install epel-release -y
    sudo yum install ansible -y
    SHELL
    end
- Step 6 - Save & check its a valid vagrantfile vagrant validate Then run
  command vagrant up to start the VM
- Step 7 - Once the VM is up and running, connect to it using SSH by running the
  command vagrant ssh
  Check ansible is installed - ansible --version
- Step 8 - Create a new directory for your Ansible project on the controller VM by
  running the command mkdir ansible-project
- Step 9 - Navigate to the ansible-project directory and create a new file called
  hosts by running the command touch hosts
- Step 10 - Create a new file called playbook.yml. This file will contain the tasks
  you want to perform on your managed hosts
  As of now the hosts and the playbook file are empty
  We will now create some host machines that will be controlled by the Ansible
  controller

## Part B - Ansible Host Machines Setup

- Step 1 - On terminal navigate to your Ansible Project folder
- Step 2 - Create a new directory for your host machines by running the
  command 
- Step 3 - Navigate to host-machines directory and create a new Vagrantfile by
 running the command vagrant init centos/7
 Step 4 - Edit the Vagrantfile and modify the following lines to set up two
 Vagrant machines:

Vagrantfile for creating VMs for Ansible Host

                Vagrant.configure("2") do |config|
                config.vm.box = "centos/7"
                config.vm.define "web" do |web|
                web.vm.hostname = "web"
                web.vm.network "private_network", ip: "192.168.33.10"
                end
                config.vm.define "db" do |db|
                db.vm.hostname = "db"
                db.vm.network "private_network", ip: "192.168.33.11"
                end
                config.vm.network "forwarded_port", guest: 80, host: 8080, auto_correct: true
                config.vm.usable_port_range = (8000..9000)
                end
                
- Step 6 - Save & check its a valid vagrantfile vagrant validate Then run
  command vagrant up to start the VM
- Step 7 - Check the status of machines vagrant status

Once the VMs are up, connect to them using SSH vagrant ssh <machine-
name> e.g vagrant ssh web

This completes the process of setting up host machines
  

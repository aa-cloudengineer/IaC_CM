#  What is Ansible? 


Ansible as a tool can be categorized in automation, server management, provisioning, and configuration management and it would pass with flying colors as all of the above. 
The reason is the ability to adapt through regular integrations with ever-evolving technologies.

Ansible can be used to install software, automate daily tasks, provision infrastructure and network components, improve security and compliance, patch systems, and orchestrate complex workflows.
Ansible is an open source IT automation engine that automates provisioning, configuration management, application deployment, orchestration, and many other IT processes.


# What makes Ansible different?

When overseeing the administration of a network comprising many (say 100) servers via configuration management tools such as Puppet, Chef, or Salt Stack the conventional approach involves installing agents on each of these machines. However, with Ansible, this step is no longer required. Ansible uses established connections specific to specific operating systems; for Linux environments, it employs SSH, while for Windows systems, it uses winRM. This makes it simpler and easy to use.

Another plus point would be its "no residual software" policy which in simple terms is that when we write Ansible code, specifically playbooks, the process involves generating Python scripts. These scripts are then executed on a custom target, making desired changes. There is no residual or left-out software residue on either the target system or the control machine (the machine on which Ansible is running), making Ansible clean and efficient in execution.

And since it's based essentially on Python libraries, we can simply get started with a pip install command, along with other ways of course. This along with YAML being the standard in writing Ansible playbooks (a list of tasks) makes it a very "friendly" tool.

# Installation 

## Prerequisites
One Ansible Control Node: The Ansible control node is the machine we’ll use to connect to and control the Ansible hosts over SSH. 
One or more Ansible Hosts: An Ansible host is any machine that your Ansible control node is configured to automate

## Step 1 — Installing Ansible

To begin using Ansible as a means of managing your server infrastructure, you need to install the Ansible software on the machine that will serve as the Ansible control node.
From your control node, run the following command:

$ sudo apt-add-repository ppa:ansible/ansible
$ sudo apt update
$ sudo apt install ansible

 ## Step 2 — Setting Up the Inventory File 

The inventory file contains information about the hosts you’ll manage with Ansible.
To edit the contents of your default Ansible inventory, open the /etc/ansible/hosts file using your text editor of choice (nano,Vim, Vi), on your Ansible control node:

$ sudo nano /etc/ansible/hosts 

The following example defines a group named [servers] with three different servers in it, each identified by a custom alias: server1, server2, and server3.
[servers]
server1 ansible_host=x.x.x.111
server2 ansible_host=x.x.x.112
server3 ansible_host=x.x.x.113

To check your inventory, you can run:
$ ansible-inventory --list -y

Make hosts SSH accessible
$ ssh-keygen
$ ssh-copy-id server1 && ssh-copy-id server2 && ssh-copy-id server3

Now that we’ve configured the inventory file, SSH connections, we have everything we need to test the connection to our Ansible hosts.

## Step 3 — Testing Connection

After setting up the inventory file to include your servers, it’s time to check if Ansible is able to connect to these servers and run commands via SSH.
You can use the -u argument to specify the remote system user. When not provided, Ansible will try to connect as your current system user on the control node.

From your local machine or Ansible control node, run:

$ ansible all -m ping -u root

Once you get a "pong" reply back from a host, it means you’re ready to run Ansible commands and playbooks on that server.

Step 4 — Running Ad-Hoc Commands (Optional)
Any command that you would normally execute on a remote server over SSH can be run with Ansible on the servers specified in your inventory file. As an example, you can check disk usage on all servers with:

$ ansible all -a "df -h" -u root

Another example, here’s how we can use the apt module to install the latest version of vim on all the servers in your inventory:
$ ansible all -m apt -a "name=vim state=latest" -u root

how you would check the uptime of every host in the servers group:
$ ansible servers -a "uptime" -u root 

specify multiple hosts by separating them with colons:
ansible server1:server2 -m ping -u root

# Ansible architecture


## Modules
Ansible works by connecting to nodes (or hosts) and pushing out small programs called modules to these nodes. Nodes are the target endpoints—servers, network devices, or any computer—that you aim to manage with Ansible. Modules are used to accomplish automation tasks in Ansible. These programs are written to be resource models of the desired state of the system. Ansible then executes these modules and removes them when finished.

## Agentless automation 

Ansible is agentless, which means the nodes it manages do not require any software to be installed on them. Ansible reads information about which machines you want to manage from your inventory. Ansible has a default inventory file, but you can create your own and define which servers you want to be managed. 

Ansible uses SSH protocol to connect to servers and run tasks. By default, Ansible uses SSH keys with ssh-agent and connects to remote machines using your current user name. Root logins are not required. You can log in as any user, and then use su or sudo commands as any user.

Once it has connected, Ansible transfers the modules required by your command or Ansible Playbook to the remote machine(s) for execution. Ansible uses human-readable YAML templates so users can program repetitive tasks to happen automatically without having to learn an advanced programming language.

## Using Ansible for ad-hoc commands 

You can also use Ansible to run ad-hoc commands, which automate a single task on one or more managed nodes. To do this, you will need to run a command or call a module directly from the command line. No playbook is used, and ad-hoc commands are not reusable. This is fine for a one-time task, but anything more frequent or complex will require the use of an Ansible Playbook.

## Ansible Playbooks
Ansible Playbooks are used to orchestrate IT processes. A playbook is a YAML file—which uses a .yml or .yaml extension—containing 1 or more plays, and is used to define the desired state of a system. This differs from an Ansible module, which is a standalone script that can be used inside an Ansible Playbook. 

Plays consist of an ordered set of tasks to execute against host selections from your Ansible inventory file. Tasks are the pieces that make up a play and call Ansible modules. In a play, tasks are executed in the order in which they are written.

When Ansible runs, it can keep track of the state of the system. If Ansible scans a system and finds the playbook description of a system and the actual system state don't agree, then Ansible will make whatever changes are necessary for the system to match the playbook. 

Ansible includes a check mode which allows you to validate playbooks and ad-hoc commands before making any state changes on a system. This shows you what Ansible would do, without actually making any changes. Handlers in Ansible are used to run a specific task only after a change has been made to the system. They are triggered by tasks and run once, at the end of all of the other plays in the playbook.

Playbook Structure(pics)

##  The Different YAML Tags

Let us now go through the different YAML tags. The different tags are described below −

- name:
This tag specifies the name of the Ansible playbook. As in what this playbook will be doing. Any logical name can be given to the playbook.

- hosts:
This tag specifies the lists of hosts or host group against which we want to run the task. The hosts field/tag is mandatory. It tells Ansible on which hosts to run the listed tasks. The tasks can be run on the same machine or on a remote machine. One can run the tasks on multiple machines and hence hosts tag can have a group of hosts’ entry as well.

- vars:
Vars tag lets you define the variables which you can use in your playbook. Usage is similar to variables in any programming language.

- tasks:
All playbooks should contain tasks or a list of tasks to be executed. Tasks are a list of actions one needs to perform. A tasks field contains the name of the task. This works as the help text for the user. It is not mandatory but proves useful in debugging the playbook. Each task internally links to a piece of code called a module. A module that should be executed, and arguments that are required for the module you want to execute.

##  Terms used in Ansible 

- Ansible Server: 	It is a machine where Ansible is installed and from which all tasks and playbooks will be executed.
- Modules: The module is a command or set of similar commands which is executed on the client-side.
- Task:           	A task is a section which consists of a single procedure to be completed.
- Role:           	It is a way of organizing tasks and related files to be later called in a playbook.
- Fact:           	The information fetched from the client system from the global variables with the gather facts operation.
- Inventory:      	A file containing the data regarding the Ansible client-server.
- Play:           	It is the execution of the playbook.
- Handler:        	The task is called only if a notifier is present.
- Notifier:       	The section attributed to a task which calls a handler if the output is changed.
- Tag:            	It is a name set to a task that can be used later on to issue just that specific task or group of jobs.

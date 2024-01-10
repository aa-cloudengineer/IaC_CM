# Ansible
Ansible can be used to install software, automate daily tasks, provision infrastructure and network components, improve security and compliance, patch systems, and orchestrate complex workflows.
Ansible is an open source IT automation engine that automates provisioning, configuration management, application deployment, orchestration, and many other IT processes.

# How does Ansible work?

## Modules
Ansible works by connecting to nodes (or hosts) and pushing out small programs—called modules—to these nodes. Nodes are the target endpoints—servers, network devices, or any computer—that you aim to manage with Ansible. Modules are used to accomplish automation tasks in Ansible. These programs are written to be resource models of the desired state of the system. Ansible then executes these modules and removes them when finished.

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


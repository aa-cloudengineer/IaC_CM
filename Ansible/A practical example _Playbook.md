
# A practical example of an Ansible Playbook
Ansible is capable of communicating with many different device classifications, from cloud-based REST APIs, to Linux and Windows systems, networking hardware, and much more. This is a sample of 2 Ansible modules automatically updating 2 types of servers:

![ansible-example](https://github.com/aa-cloudengineer/IaC/assets/144057103/7a0b1227-6c70-4630-8c9e-c1bf21e33040)

## The playbook contains 2 plays: 

The first checks whether or not web server software is up to date and runs the update if necessary.
The second checks whether or not database server software is up to date and runs the update if necessary.

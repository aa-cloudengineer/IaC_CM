
# A practical example of an Ansible Playbook
Ansible is capable of communicating with many different device classifications, from cloud-based REST APIs, to Linux and Windows systems, networking hardware, and much more. This is a sample of 2 Ansible modules automatically updating 2 types of servers:

---
- name: Update web servers
  hosts: webservers
  become: true
 
  tasks:
    - name: Ensure apache is at the latest version
      ansible.builtin.yum:
        name: httpd
        state: latest
    - name: Write the apache config file
      ansible.builtin.template:
        src: /srv/httpd.j2
        dest: /etc/httpd.conf
        mode: "0644"
 
- name: Update db servers
  hosts: databases
  become: true
 
  tasks:
    - name: Ensure postgresql is at the latest version
      ansible.builtin.yum:
        name: postgresql
        state: latest
    - name: Ensure that postgresql is started
      ansible.builtin.service:
        name: postgresql
        state: started
============================================================================      
## The playbook contains 2 plays: 

The first checks whether or not web server software is up to date and runs the update if necessary.
The second checks whether or not database server software is up to date and runs the update if necessary.

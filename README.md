# Ansible Role: Apache Server Deployment

This Ansible role deploys an Apache server in a Docker container on an Ubuntu system. It ensures all necessary dependencies are installed, sets up Docker and Docker Compose, and creates a simple web page served by the Apache server.

## Requirements

- Ansible 2.16 or later
- Ubuntu 18.04/20.04/22.04/24.04
- Docker and Docker Compose

## Role Variables

The variables required by this role are defined in `defaults/main.yml`:

- System user for the role operations: 
  -  system_user: ubuntu

- Name of the Docker container to run the Apache server
    - container_name: webapp_container

- Ports to expose on the Apache container
    - exposed_ports: "80:80"

-  Destination path for the index.html template file on the client system
      - template_dest: /home/ubuntu/index.html

- Welcome message to be displayed on the index.html
    - welcome: "{{ system_user }}"

## Usage
1. Clone this repository to your Ansible roles directory.
2. Create a playbook that uses this role
```
---
- hosts: prod
  become: true
  roles:
    - ansible-role-webapp
```
3. Define the inventory file, hosts.yml for the target hosts:
  ```yml
all:
  vars:
    ansible_ssh_common_args: '-o StrictHostKeyChecking=no'

prod:
  hosts:
    client:
      ansible_host: *.*.*.*
      ansible_user: ubuntu
      ansible_ssh_private_key_file: /path/to/your/private/key
```
4. Run the playbook:
   ```
   ansible-playbook -i inventory_file your_playbook.yml
   ``` 
## Conclusion:
This mini-project showcases an Ansible role that deploys an Apache server in a Docker container on Ubuntu. It automates the installation of dependencies, Docker setup, and Apache container configuration, simplifying web server deployment and management.

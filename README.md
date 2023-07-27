# Ansible Server Management

The [ansible repository][ansible-servermanagement-repository-url] will store all code related to ansible. This repository is also used by Jenkins server to automate deployments.

## Tools used

* [![Ansible][ansible-img]][ansible-url]
* [![Python][python-img]][python-url]

## Now What?

### Notes

* This repository is to keep all ansible configuration and roles. It include all ansible configuration files.

### Security Requriements

Before running any ansible playbook, a password protected SSH-KEY should be created. Follow this [guide][how-to-set-up-ssh-key-guide-url] to create yourself a SSH key.

Once the key is generate, have someone with access to server create you a user account and update the user with your public ssh key.

### Installation (CensOS)

Step1. Install [Ansible][ansible-help-url]. It will install ansible-core with required dependencies.

    ```shell
    #Install ansible-core onto your CentOS box
    sudo dnf install ansible-core
    ``` 

Step2. Clone the repository to your computer.

    ```shell
    # Clone the repository and place it where ever you would like
    git clone git@github.com:akphero/ansible.git
    ``` 

Step3. Modify the ansible.cfg by uncommending the log path. This will enable logging on your local computer, but it will disable uploading the config file.

    ```shell
    #Enable ansible logging
    sed -i 's/#log_path/log_path/' ansible.cfg
    ``` 

Step4. Exclude ansible.cfg from being uploaded to the repository.

    ```shell
    #Exclude ansible.cfg from git updates
    git update-index --assume-unchanged ansible.cfg
    ``` 

### Ansible Basics

Inside a playbooks[ansible-playbooks-url] folder, playbooks are created based on requests. If you want a certain playbook created. Please reach out to me on [linkedin][linked-in-url]. 

The [inventory][ansible-hosts-config-url] folder keeps all hosts information for every server. It must be updated and keep it up to date in order for [roles][ansible-roles-url] and [playbooks][ansible-playbooks-url] to work correctly.

### Examples

Example1: To find information about a spefic host.

    ```shell
    #Check if host is available
    ansible -m ping SAMPLE-SERVER
    #List all information about the server
    ansible -m setup SAMPLE-SERVER
    ``` 

Example: Sample playbook configuration


        ---
        # This playbook configures a new server with whatever role is enabled.
        #- hosts: SAMPLE-SERVER
        roles:
        #    - { role: roles/sysinfo }
        #    - { role: roles/common }
        #    - { role: roles/enable-repo }
        #    - { role: roles/install-application }
        #    - { role: roles/sophos }
        #    - { role: roles/os-update }    
        #    - { role: roles/docker-install }
        #    - { role: roles/docker-redis }
        #    - { role: roles/docker-smtp-container }
        #    - { role: roles/system-environment-variables }
        #    - { role: roles/update-ssh-keys }
        #    - { role: roles/zabbix-update-custom-parameters }
        #    - { role: roles/install-application }
        #    - { role: roles/reboot }

Example2: How to run a playbook again a new server. 

1. Make sure you add a new server information to the [hosts][ansible-hosts-file-url] file. 

2. Make sure to add a [hosts vars][ansible-hosts-vars-file-url] file.

3. Modify the new server installation yml file by specifying the host name and uncommeting the roles that you want to run against the host and run the playbook.

    ```shell
    #add host information to execute on and which roles to run
    nano playbooks/manual/all/new_server_installation.yml
    #run the playbook
    ansible-playbook playbooks/new_server_installation.yml
    ``` 

### Resource for Ansible

* Ansible common command lines: [https://docs.ansible.com/ansible/latest/command_guide/index.html](https://docs.ansible.com/ansible/latest/command_guide/index.html)
* Ansible Getting Started: [https://docs.ansible.com/ansible/latest/getting_started/index.html](https://docs.ansible.com/ansible/latest/getting_started/index.html)


<!-- MARKDOWN LINKS & IMAGES -->

[ansible-servermanagement-repository-url]: https://github.com/akphero/ansible
[ansible-img]: https://img.shields.io/badge/ansible-000000?style=for-the-badge&logo=ansible
[ansible-url]: https://www.ansible.com/
[ansible-help-url]:https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html
[python-img]: https://img.shields.io/badge/python-000000?style=for-the-badge&logo=python
[python-url]: https://www.python.org/
[ansible-hosts-config-url]: https://github.com/akphero/ansible/tree/master/inventory
[ansible-playbooks-url]: https://github.com/akphero/ansible/tree/master/playbooks/
[ansible-roles-url]: https://github.com/akphero/ansible/tree/master/roles
[ansible-hosts-file-url]: https://github.com/akphero/ansible/blob/master/inventory/hosts
[ansible-hosts-vars-file-url]: https://github.com/akphero/ansible/tree/master/inventory/host_vars
[how-to-set-up-ssh-key-guide-url]: https://git-scm.com/book/en/v2/Git-on-the-Server-Generating-Your-SSH-Public-Key
[linked-in-url]: https://www.linkedin.com/in/aleksandrkarnafel/
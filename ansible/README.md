# Ansible

## Introduction

Ansible is simple open source IT engine which automates application deployment, intra service orchestration, cloud provisioning and many other IT tools.

Ansible is easy to deploy because it does not use any agents or custom security infrastructure.

Ansible uses playbook to describe automation jobs, and playbook uses very simple language i.e. YAML (It’s a human-readable data serialization language & is commonly used for configuration files, but could be used in many applications where data is being stored)which is very easy for humans to understand, read and write. Hence the advantage is that even the IT infrastructure support guys can read and understand the playbook and debug if needed (YAML – It is in human readable form).

Ansible is designed for multi-tier deployment. Ansible does not manage one system at time, it models IT infrastructure by describing all of your systems are interrelated. Ansible is completely agentless which means Ansible works by connecting your nodes through ssh(by default). But if you want other method for connection like Kerberos, Ansible gives that option to you.

After connecting to your nodes, Ansible pushes small programs called as “Ansible Modules”. Ansible runs that modules on your nodes and removes them when finished. Ansible manages your inventory in simple text files (These are the hosts file). Ansible uses the hosts file where one can group the hosts and can control the actions on a specific group in the playbooks.

### Sample Hosts File
This is the content of hosts file −

<pre>
    #File name: hosts
    #Description: Inventory file for your application. Defines machine type abc
    node to deploy specific artifacts
    # Defines machine type def node to upload
    metadata.

    [abc-node]
    #server1 ansible_host = <target machine for DU deployment> ansible_user = <Ansible
    user> ansible_connection = ssh
    server1 ansible_host = <your host name> ansible_user = <your unix user>
    ansible_connection = ssh

    [def-node]
    #server2 ansible_host = <target machine for artifact upload>
    ansible_user = <Ansible user> ansible_connection = ssh
    server2 ansible_host = <host> ansible_user = <user> ansible_connection = ssh
</pre>

### What is Configuration Management

Configuration management in terms of Ansible means that it maintains configuration of the product performance by keeping a record and updating detailed information which describes an enterprise’s hardware and software.

Such information typically includes the exact versions and updates that have been applied to installed software packages and the locations and network addresses of hardware devices. For e.g. If you want to install the new version of WebLogic/WebSphere server on all of the machines present in your enterprise, it is not feasible for you to manually go and update each and every machine.

You can install WebLogic/WebSphere in one go on all of your machines with Ansible playbooks and inventory written in the most simple way. All you have to do is list out the IP addresses of your nodes in the inventory and write a playbook to install WebLogic/WebSphere. Run the playbook from your control machine & it will be installed on all your nodes.

### How Ansible Works?

The picture given below shows the working of Ansible.

Ansible works by connecting to your nodes and pushing out small programs, called "Ansible modules" to them. Ansible then executes these modules (over SSH by default), and removes them when finished. Your library of modules can reside on any machine, and there are no servers, daemons, or databases required.

![Ansible Architecture](https://www.tutorialspoint.com/ansible/images/ansible_works.jpg)

The management node in the above picture is the controlling node (managing node) which controls the entire execution of the playbook. It’s the node from which you are running the installation. The inventory file provides the list of hosts where the Ansible modules needs to be run and the management node does a SSH connection and executes the small modules on the hosts machine and installs the product/software.

**Beauty of Ansible is that it removes the modules once those are installed so effectively it connects to host machine , executes the instructions and if it’s successfully installed removes the code which was copied on the host machine which was executed.**

## AD HOC Commands

Ad hoc commands are commands which can be run individually to perform quick functions. These commands need not be performed later.

For example, you have to reboot all your company servers. For this, you will run the Adhoc commands from ‘/usr/bin/ansible’.

These ad-hoc commands are not used for configuration management and deployment, because these commands are of one time usage.

A typical example for copying a file in the host machine `ansible localhost -m copy -a "src=./test1/sample.txt dest=./test2"`.

You can use the modules explicitly here.

## Playbooks

Playbooks are the files where Ansible code is written. Playbooks are written in YAML format. YAML stands for Yet Another Markup Language. Playbooks are one of the core features of Ansible and tell Ansible what to execute. They are like a to-do list for Ansible that contains a list of tasks.

Playbooks contain the steps which the user wants to execute on a particular machine. Playbooks are run sequentially. Playbooks are the building blocks for all the use cases of Ansible.

### Playbook Structure

Each playbook is an aggregation of one or more plays in it. Playbooks are structured using Plays. There can be more than one play inside a playbook.

The function of a play is to map a set of instructions defined against a particular host.

YAML is a strict typed language; so, extra care needs to be taken while writing the YAML files. There are different YAML editors but we will prefer to use a simple editor like notepad++. Just open notepad++ and copy and paste the below yaml and change the language to YAML (Language → YAML).

A YAML starts with --- (3 hyphens)

### Create a Playbook

Let us start by writing a sample YAML file. We will walk through each section written in a yaml file.

<pre>
   name: install and configure DB
   hosts: testServer
   become: yes

   vars: 
      oracle_db_port_value : 1521
   
   tasks:
   -name: Install the Oracle DB
      yum: code to install db
    
   -name: Ensure the installed service is enabled and running
   service:
      name: service name
</pre>

The above is a sample Playbook where we are trying to cover the basic syntax of a playbook. Save the above content in a file as test.yml. A YAML syntax needs to follow the correct indentation and one needs to be a little careful while writing the syntax.

### The Different YAML Tags

Let us now go through the different YAML tags. The different tags are described below −

### name

This tag specifies the name of the Ansible playbook. As in what this playbook will be doing. Any logical name can be given to the playbook.

### hosts

This tag specifies the lists of hosts or host group against which we want to run the task. The hosts field/tag is mandatory. It tells Ansible on which hosts to run the listed tasks. The tasks can be run on the same machine or on a remote machine. One can run the tasks on multiple machines and hence hosts tag can have a group of hosts’ entry as well.

### vars

Vars tag lets you define the variables which you can use in your playbook. Usage is similar to variables in any programming language.

### tasks

All playbooks should contain tasks or a list of tasks to be executed. Tasks are a list of actions one needs to perform. A tasks field contains the name of the task. This works as the help text for the user. It is not mandatory but proves useful in debugging the playbook. Each task internally links to a piece of code called a module. A module that should be executed, and arguments that are required for the module you want to execute.

## Ansible Roles

Roles provide a framework for fully independent, or interdependent collections of variables, tasks, files, templates, and modules.

In Ansible, the role is the primary mechanism for breaking a playbook into multiple files. This simplifies writing complex playbooks, and it makes them easier to reuse. The breaking of playbook allows you to logically break the playbook into reusable components.

Each role is basically limited to a particular functionality or desired output, with all the necessary steps to provide that result either within that role itself or in other roles listed as dependencies.

Roles are not playbooks. Roles are small functionality which can be independently used but have to be used within playbooks. There is no way to directly execute a role. Roles have no explicit setting for which host the role will apply to.

Top-level playbooks are the bridge holding the hosts from your inventory file to roles that should be applied to those hosts.

### Creating a role

The directory structure for roles is essential to create a new role.

- ### Role Structure
    Roles have a structured layout on the file system. The default structure can be changed but for now let us stick to defaults.

    Each role is a directory tree in itself. The role name is the directory name within the /roles directory.

    `$ ansible-galaxy -h `

    Usage

    `ansible-galaxy [delete|import|info|init|install|list|login|remove|search|setup] [--help] [options] ...`

    Options
    <pre>
    -h, --help − Show this help message and exit.

    -v, --verbose − Verbose mode (-vvv for more, -vvvv to enable connection debugging)

    --version − Show program's version number and exit.
    </pre>

- ### Creating a Role Directory
    The above command has created the role directories.

    <pre>
        $ ansible-galaxy init vivekrole 
        ERROR! The API server (https://galaxy.ansible.com/api/) is not responding, please try again later. 

        $ ansible-galaxy init --force --offline vivekrole 
        - vivekrole was created successfully 
    </pre>
    <pre>
        $ tree vivekrole/ 
        vivekrole/ 
        ├── defaults 
        │   └── main.yml 
        ├── files ├── handlers 
        │   └── main.yml 
        ├── meta 
        │   └── main.yml 
        ├── README.md ├── tasks 
        │   └── main.yml 
        ├── templates ├── tests │   ├── inventory 
        │   └── test.yml 
        └── vars 
            └── main.yml 
        
        8 directories, 8 files
    </pre>
    Not all the directories will be used in the example and we will show the use of some of them in the example.

- ### Utilizing Roles in Playbook
    
    This is the code of the playbook we have written for demo purpose. This code is of the playbook vivek_orchestrate.yml. We have defined the hosts: tomcat-node and called the two roles – install-tomcat and start-tomcat.

    The problem statement is that we have a war which we need to deploy on a machine via Ansible.
    <pre>
        --- 
        - hosts: tomcat-node 
        roles: 
        - {role: install-tomcat} 
        - {role: start-tomcat} 
    </pre>

    <pre>
        $ ls 
        ansible.cfg  hosts  roles  vivek_orchestrate.retry vivek_orchestrate.yml 
    </pre>

    There is a tasks directory under each directory and it contains a main.yml. The main.yml contents of install-tomcat are −
    
    <pre>
        --- 
        #Install vivek artifacts 
        -  
        block: 
            - name: Install Tomcat artifacts
                action: > 
                    yum name = "demo-tomcat-1" state = present 
                register: Output 
                
        always: 
            - debug: 
                msg: 
                    - "Install Tomcat artifacts task ended with message: {{Output}}" 
                    - "Installed Tomcat artifacts - {{Output.changed}}" 
        The contents of main.yml of the start tomcat are −

        #Start Tomcat          
        -  
        block: 
            - name: Start Tomcat 
            command: <path of tomcat>/bin/startup.sh" 
            register: output 
            become: true 
        
        always: 
            - debug: 
                msg: 
                    - "Start Tomcat task ended with message: {{output}}" 
                    - "Tomcat started - {{output.changed}}" 
    </pre>
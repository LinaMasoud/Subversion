# End-To-End Subversion Installation with ldap Configuration 
This is a playbook with a couple of roles and tasks to install and configure Apache SVN Server from Scratch 

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing or even production purposes.

### Prerequisites & Steps to Run the playbook
1) 2 RedHat/CentOS7 machines (Ansible Controller - SVN Server)
2) Install Ansible on the Controller using the following commands:
```
sudo yum install epel-release
sudo yum install ansible
```
3) Setup Ansible ServiceAccount & SSH Configuration:
    On the Controller & SVN Server:
    ```
        sudo -i
        mkdir /ansiblesvc
        useradd ansiblesvc -md /ansiblesvc
        chown -R ansiblesvc:ansiblesvc /ansiblesvc
        usermod --shell /bin/bash ansiblesvc
     ```
  On the Controller:
  ```
    su - ansiblesvc
    ssh-keygen
    Copy the Public Key exist in .ssh/id_rsa.pub
  ```
  On SVN Server:
  ```
    su - ansiblesvc
    mkdir .ssh
    chmod 700 .ssh
    touch authorized_keys
    Paste the public key in authorized_keys
    chmod 644 authorized_keys
  ```
4) From The controller Clone the Playbook & Change Directory to the files
5) Run the playbook after updating hosts & group_var/all.yml files carefully using the following command:
```
    su - ansiblesvc 
    ansible-playbook -i hosts svn.yml
```
6) Verify the provisioning
```
    cd  /svn-repository
    mkdir test
    /usr/local/bin/make-svn-repository -r <testrepo> -s test -o "your name" -c "comment"
    Check the repo from the browser
```

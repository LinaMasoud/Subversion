# Subversion

To Build Subversion Server from Scratch using Ansible Playbook you need:

1) 2 RedHat/CentOS7 machines (Ansible Controller - SVN Server)
2) Install Ansible on the Controller using the following commands:
  # sudo yum install epel-release
  # sudo yum install ansible
3) Setup Ansible ServiceAccount & SSH Configuration:
  # On the Controller & SVN Server:
    sudo -i
    mkdir /ansiblesvc
    useradd ansiblesvc -md /ansiblesvc
    chown -R ansiblesvc:ansiblesvc /ansiblesvc
    usermod --shell /bin/bash ansiblesvc
  # On the Controller:
    su - ansiblesvc
    ssh-keygen
    Copy the Public Key exist in .ssh/id_rsa.pub
  # On SVN Server:
    su - ansiblesvc
    mkdir .ssh
    chmod 700 .ssh
    touch authorized_keys
    Paste the public key in authorized_keys
    chmod 644 authorized_keys
4) From The controller Clone the Playbook & Change Directory to the files
5) Run the playbook after updating hosts & group_var/all.yml files carefully using the following command:
  # su - ansiblesvc
  # ansible-playbook -i hosts svn.yml
6) Verify the provisioning
  # cd  /svn-repository
  # mkdir test
  # /usr/local/bin/make-svn-repository -r <testrepo> -s test -o "your name" -c "comment"
  # Check the repo from the browser
###########################################################################################################
  Update the hosts file with your SVN Server hostname
# cat hosts
[svn]
your_hostname
###########################################################################################################
  Update the group_vars/all.yml file with your values
#cat group_vars/all.yml
---
service_account: <local_serviceaccount_name>
AuthLDAPBindDN: <ldap_serviceaccount_name>
AuthLDAPBindPassword: <ldap_serviceaccount_password>
AuthLDAPURL: <ldap_url>
shared_area: <your_sharedarea_on_filer>

# Ansible playbook for Wordpress

## Install 

Edit the host_vars/ files and ansible.cfg to match your hosts.

Then you can start the playbooks in the this order :

```
ansible-playbook plays/database.yml
ansible-playbook plays/web-package.yml
ansible-playbook plays/wordpress.yml
```

Now you have the Wordpress installation page at your web-server ip.

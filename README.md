Drupal install & config ansible playbook
========================================

This repository contains an ansible playbook, that will install a ready-to-use, working Drupal site on your machines.  
But it's not only an ansible playbook, it is working together with my cloud-manager tool.

So you can choose from one of these options, to use it:

1. Using the cloud-manager
2. Using only ansible

**Note: This playbook is intended to use only on fresh installs, as it modifies the apache configuration.**


1. Using the cloud-manager
--------------------------
  1.1. Install the cloud-manager gem

   ```
   $ gem install cloud_manager
   ```
   
  1.2. Run your cloud-manager configuration
  
   ```
   $ cloud_manager manage my_configuration.yml
   ```
   
   Some sample cloud-manager configuration files added under the cloud-manager directory.  
   The cloud-manager will provide the inventory file for the playbook to use, and it will start the playbook as well.  
   Detailed information on how to use and make a configuration file for the cloud-manager, can be found in the [cloud-manager's documentation](https://github.com/smatyas/cloud-manager).
   
   **IMPORTANT: although default values are provided, you should ALWAYS override the default passwords in your cloud-manager config.**
   
   The default settings and credentials can be found in the [drupal role defaults](drupal/defaults/main.yml). These variables can be overridden in your cloud-manager config. See the examples!
  
   
  1.3. Set environment variables (optional)
   
   Depending on your setup, environment variables should be set, to make the cloud-manager run correctly, and to provide nice output.  
   I.e. to provide colored output in the ansible running stage, and to prevent host key checking, run something like this:
   
   ```
   $ ANSIBLE_FORCE_COLOR=true ANSIBLE_HOST_KEY_CHECKING=false AWS_REGION=eu-central-1 cloud_manager manage my_configuration.yml
   ```
   
   
2. Using only ansible
---------------------

As for other ansible playbooks to use, use should provide your inventory file.  
The playbook will install all the dependencies and softwares needed to run Drupal.  
Using drush, it configures a ready-to-use drupal instance with an admin user. 

The default settings and credentials can be found in the [drupal role defaults](drupal/defaults/main.yml).

**IMPORTANT: although default values are provided, you should ALWAYS override the passwords, i.e. using hostvars.**

The playbook installs drupal on hosts in the `drupal_hosts` hostgroup.

Running the playbook:

```
$ ansible-playbook -i my_hosts site.yml
```
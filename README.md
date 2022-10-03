# Vagrant Setup
### Export environment variables
#### Ansible PLaybook Name
```
    export PLAYBOOK=[PLAYBOOK_NAME]
```
#### VARS File Ansible Override Vars File
```
    export EXTRA_VARS=[EXTRA_VARS]
```
### Initialize the VMs
```
    vagrant up --provision 
```
### SSH in the provisioned VMs
```
    vagrant ssh kube1
    vagrant ssh kube2
    vagrant ssh kube3
```
### Destroy the VMs
```
    vagrant destroy -f 
```

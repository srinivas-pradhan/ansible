# Run Ansible Playbook 
```
ansible-playbook --extra-vars @[EXTRA_VARS_FILE] [PLAYBOOK_NAME]
```

# Vagrant Setup
### Export environment variables
#### Ansible Playbook Name
```
    export PLAYBOOK=[PLAYBOOK_NAME]
```
#### VARS File (Ansible Override Vars File)
```
    export EXTRA_VARS=[EXTRA_VARS]
```
### Initialize the VMs
```
    vagrant up --provision 
```
### SSH in the provisioned VMs
```
    vagrant ssh [VM_NAME]
```
### Destroy the VMs
```
    vagrant destroy -f 
```

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
#### AWS Provisioner Setup
```
export AWS_PROFILE=[AWS_PROFILE]
export KEY_PAIR_NAME=[KEY_PAIR_NAME]
export REGION=[REGION]
export AMI=[AMI]
export SG_ID=[SG_ID]
export SUBNET_ID=[SUBNET_ID]
export PRIVATE_KEY_PATH=[PRIVATE_KEY_PATH]
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

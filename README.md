# Ansible MSAzure Web Application
[Reference1](https://docs.microsoft.com/en-us/azure/developer/ansible/vm-configure?tabs=ansible)
Create an SSH key pair
```
ssh-keygen -m PEM -t rsa -b 4096
```
```
cat ~/.ssh/id_rsa.pub
```
Run Ansible
```
ansible-playbook vm.yaml
```


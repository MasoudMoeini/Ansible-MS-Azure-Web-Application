# Ansible MSAzure Web Application
[Refrence1](https://docs.microsoft.com/en-us/azure/developer/ansible/install-on-linux-vmtabs=azure-cli#install-ansible-on-an-azure-linux-virtual-machine)<br/>
[Reference2](https://docs.microsoft.com/en-us/azure/developer/ansible/vm-configure?tabs=ansible)<br/>
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


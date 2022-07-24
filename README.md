# Ansible MSAzure Web Application
[Reference 1](https://docs.microsoft.com/en-us/azure/developer/ansible/install-on-linux-vmtabs=azure-cli#install-ansible-on-an-azure-linux-virtual-machine)<br/>
[Reference 2](https://docs.microsoft.com/en-us/azure/developer/ansible/vm-configure?tabs=ansible)<br/>
Deploying Flask Web Application to Linux (centos 7.7.1908) vitual Machine in MS-Azure<br>
[Reference 3](https://dev.to/cloudskills/deploy-a-windows-vm-to-azure-with-ansible-2l9m)
```
az login
```
```
openssl rand -hex 6
ssh-keygen -t ed25519 -f ~/.ssh/ansbile_8f4f13923647 -C ansible-flask-web-app
cat ~/.ssh/ansbile_8f4f13923647 >> private.key
```
```
ansible-playbook ansible-azure-vm.yaml -vvv
```
# Manually set up 
Configure Linux Machine on Azure<br/>
``` 
az group create --name QuickstartAnsible-rg --location eastus
```
```
az vm create \
--resource-group QuickstartAnsible-rg \
--name QuickstartAnsible-vm \
--image OpenLogic:CentOS:7.7:latest \
--admin-username azureuser \
--admin-password 
```
Get the public Ip address of the Azure virtual machine
```
az vm show -d -g QuickstartAnsible-rg -n QuickstartAnsible-vm --query publicIps -o tsv
```
Create ssh pair key and Connect to your virtual machine via SSH
```
openssl rand -hex 6
ssh-keygen -t ed25519 -f ~/.ssh/ansbile_8f4f13923647 -C ansible-flask-web-app
cat ~/.ssh/ansbile_8f4f13923647 >> private.key
```
```
ssh azureuser@<vm_ip_address>
```
``` 
ansible-playbook -u user -i <public_ip_address>, --private-key private.key flask.yaml
```
```
Excluded
ssh-keygen -m PEM -t rsa -b 4096
cat ~/.ssh/id_rsa.pub
```
Clean up Resources
```
az group delete --name QuickstartAnsible-rg
``` 
```
az group show --name <resource_group>
```



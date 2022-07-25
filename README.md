# Ansible MSAzure Web Application
[Reference 1](https://docs.microsoft.com/en-us/azure/developer/ansible/install-on-linux-vmtabs=azure-cli#install-ansible-on-an-azure-linux-virtual-machine)<br/>
[Reference 2](https://docs.microsoft.com/en-us/azure/developer/ansible/vm-configure?tabs=ansible)<br/>
[Reference 3](https://dev.to/cloudskills/deploy-a-windows-vm-to-azure-with-ansible-2l9m)<br/>
Deploying Flask Web Application to Linux (centos 7.7.1908) vitual Machine in MS-Azure<br>
Installing Dependencies<br/>
```
pip install 'ansible[azure]'
```
```
curl -O https://raw.githubusercontent.com/ansible-collections/azure/dev/requirements-azure.txt
```
Add azure-storage==0.35.1 to the end of requirements-azure.txt
```
pip install -r requirements-azure.txt
```
```
az login
```
Creating ssh pair keys and replacing the public key value in roles/vm/tasks/main.yaml
```
ssh-keygen -m PEM -t rsa -b 4096
cat ~/.ssh/id_rsa.pub
```
```
chmod 600 /Users/masoudmoeini/.ssh/id_rsa 
```
Running ansible to create virtual machine
``` 
ansible-playbook vm.yaml
```
To get VM public IP 
```
az vm show -d -g myResourceGroup -n myVM --query publicIps -o tsv
```
To connect VM 
```
ssh azureuser@<vm_ip_address>
```
The flask application is available at below url
```
http://<vm_ip_address>:5000 
```
You should see something similar<br/>
<img width="668" alt="Screenshot 2022-07-25 at 16 24 36" src="https://user-images.githubusercontent.com/43514418/180801271-56cb3fed-3335-4a2f-8408-2a90980879a2.png"><br>
Further process
```
ansible-playbook ansible-azure-vm.yaml -vvv
```
``` 
ansible-playbook -u user -i <public_ip_address>, flask.yaml
ansible-playbook -u user -i <public_ip_address>, --private-key private.key flask.yaml
```
# Clean up Resources
```
az group delete --name myResourceGroup
``` 
```
az group show --name <resource_group>
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
--admin-password <your password>
```
Get the public Ip address of the Azure virtual machine
```
az vm show -d -g QuickstartAnsible-rg -n QuickstartAnsible-vm --query publicIps -o tsv
```
Create ssh pair key and Connect to your virtual machine via SSH
```
Excluded
openssl rand -hex 6
ssh-keygen -t ed25519 -f ~/.ssh/ansbile_8f4f13923647 -C ansible-flask-web-app
cat ~/.ssh/ansbile_8f4f13923647 >> private.key
```







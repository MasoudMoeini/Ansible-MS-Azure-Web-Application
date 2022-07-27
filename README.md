# Ansible MS Azure Web Application
[Reference 1](https://docs.microsoft.com/en-us/azure/developer/ansible/install-on-linux-vmtabs=azure-cli#install-ansible-on-an-azure-linux-virtual-machine)<br/>
[Reference 2](https://docs.microsoft.com/en-us/azure/developer/ansible/vm-configure?tabs=ansible)<br/>
[Reference 3](https://dev.to/cloudskills/deploy-a-windows-vm-to-azure-with-ansible-2l9m)<br/>
Deploying Flask Web Application to Linux --Ubuntu 18.04.6 LTS (GNU/Linux 5.4.0-1086-azure x86_64)-- vitual Machine in MS-Azure<br>
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
Installing flask web application 
```
ansible-playbook -u user -i <public_ip_address>, flask.yaml
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
<img width="630" alt="Screenshot 2022-07-25 at 16 29 06" src="https://user-images.githubusercontent.com/43514418/180801647-bc2bb874-9901-425e-9d85-bfcd3abc9b34.png"><br>

# Clean up Resources
```
az group delete --name myResourceGroup
``` 
```
az group show --name myResourceGroup
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







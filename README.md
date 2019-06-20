# Fast Automated Kubernetes Home Lab Setup with Virtualbox, Vagrant and Ansible
The purpose of this project is to build a K8S environment quickly with Virtualbox, Ansible and Vagrant.

<hr>

**Tested Environment**

- Ubuntu: 18.04.2
- Vagrant: 2.2.4
- Ansible: 2.8.1
- Virtualbox: 5.2.30

**1. Install Vagrant, Ansible and VirtualBox**

`sudo apt-get install virtualbox vagrant ansible`

**2. Initiate Vagrant**

Create a directory and run the following under it

```
vagrant box add ubuntu/bionic64
vagrant init ubuntu/bionic64
```

A file "Vagrantfile" will be created.

"ubuntu/bionic64" is referring to Ubuntu 18.04. Other OS (i.e., Vagrant Boxes) are listed on https://app.vagrantup.com/boxes/search

**3. Append IP address of your host to the end of file /etc/ansible/hosts**

![alt text](https://raw.githubusercontent.com/ipccheng/k8s-home-lab/master/Figure-1.JPG)

**4. Download and Unzip the file under the directory you have created in Step 2"**

**5. Set up the K8S Master Node on the host**

First, edit the master-playbook.yml and edit the "vars" values. The attributes are:

- home_directory
- cni_provider
- master_node_ip_address
- pod_network

Then dry run the master-playbook.yml first and edit the playbook if needed.

`ansible-playbook --connection:local master-playbook.yml --check -vvv`

If everything seems OK, run

`ansible-playbook --connection:local master-playbook.yml`

**6. Check whether the K8S master node is running**

`kubectl get nodes`

You should see the master node with STATUS "Ready"

**7. Set up the K8S Worker Nodes on VirtualBox**

Edit the new "Vagrantfile" file created in Step 4 and you may change the properties of the following attributes

- OS (default: ubunut/bionic64)
- number of Worker Nodes (default: 3)
- hostnames
- vCPU per nodes (default: 2)
- memory per nodes (default: 2GB)
- IP address range

`vagrant up`

**8. Done! Now check the status of your K8S environment"**

`kubectl get nodes`

![alt text](https://raw.githubusercontent.com/ipccheng/k8s-home-lab/master/Figure-2.JPG)

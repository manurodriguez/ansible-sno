## Playbooks to deploy Single Node Openshift on a libvirt VM

### Pre-requisites

- A RHEL 8.4 server with direct internet access
- access to base and appstream repos required. 
- ansible and git installed in your workstation where the deploy-sno.yml playbook is executed

Install the following in the hypervisor (provisioner node)
```bash
sudo dnf install -y python3-netaddr
```

Configure the following in the inventory for ansible

- user with sudo access
- ssh pub key added to user for ansible to run
- prepare hosts inventory with :
  * pull secret
  * domain
  * cluster name
  * dir to store deployment files
  * extcidrnet
  * provisioner host entry
  * proxy if required

Example:
```bash
[all:vars]
dir="{{ ansible_user_dir }}/clusterconfigs"
domain="example.com"
cluster="ocp4"
extcidrnet="192.168.126.0/24"
pullsecret="Add-your-pull-secret-in-json"
ansible_ssh_extra_args='-o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null'

[provisioner]
<IP-of-host-where-SNO-will-be-installed ansible_user=<add-your-user-name>
```

### Deploy
```bash
ansible-playbook deploy-sno.yml -i /etc/ansible/hosts 
```

### Delete
```bash
ansible-playbook deploy-sno.yml -i /etc/ansible/hosts -t cleanup
```

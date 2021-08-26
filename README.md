== Playbooks to deploy Single Node Openshift on a libvirt VM

=== Pre-requisites

- A RHEL 8.4 server with direct internet access
- access to base and appstream repos required. 
- If the vars activation_key and org_id are provided registration is done during the deployment.

Install the following in the hypervisor (provisioner node)
```bash
ansible-galaxy collection install containers.podman
ansible-galaxy collection install ansible.posix
ansible-galaxy collection install ansible.netcommon
ansible-galaxy collection install community.libvirt
```

Configure the following in the inventory for ansible

- user with sudo access
- ssh pub key added to user for ansible to run
- prepare hosts inventory with :
  * pull secret
  * domain
  * cluster name
  - dir to store deployment files
  * extcidrnet
  * provisioner host entry
  * proxy if required

=== Deploy
```bash
ansible-playbook deploy-sno.yml -i /etc/ansible/hosts 
```

=== Delete
```bash
ansible-playbook deploy-sno.yml -i /etc/ansible/hosts -t cleanup
```

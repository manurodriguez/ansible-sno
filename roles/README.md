Deploy
```bash
ansible-playbook deploy-sno.yml -i /etc/ansible/hosts 
```
Delete
```bash
ansible-playbook deploy-sno.yml -i /etc/ansible/hosts -t cleanup
```

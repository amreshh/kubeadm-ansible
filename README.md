# kubeadm-ansible

# Provision kubernetes cluster
```bash
pipenv run ansible-playbook -i inventories/vagrant.ini site.yml
```

```bash
# print facts
pipenv run ansible all -m ansible.builtin.setup
```
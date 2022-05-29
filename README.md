# kubeadm-ansible

Ansible playbook to deploy a Kubernetes cluster using kubeadmn and crio as container runtime.
# Provision kubernetes cluster
```bash
pipenv run ansible-playbook -i inventories/vagrant.ini site.yml --vault-password-file vault_password.txt
```

```bash
# print facts
pipenv run ansible all -m ansible.builtin.setup
```

## Set tokens
Create and set the tokens in [./group_vars/all/vault](./group_vars/all/vault)

On the control plane execute the following to get the tokens.
```bash
# Create token
sudo kubeadm token create

# Create discovery token CA Cert Hash
openssl x509 -pubkey \
  -in /etc/kubernetes/pki/ca.crt | openssl rsa \
  -pubin -outform der 2>/dev/null | openssl dgst \
  -sha256 -hex | sed 's/^.* //'
```
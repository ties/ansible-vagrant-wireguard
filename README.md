Ansible example: Three containers with wireguard network
--------------------------------------------------------
```
vagrant up
ansible-galaxy install -r requirements.yml
# Enter the directory with Ansible playbook:
cd ansible
ansible-playbook site.yml --ask-become-pass
```

This should bring up three containers with a wireguard network in between. The main node (default-1)
will be able to ping the others (10.8.0.{2,3}), but cross-node communication is not possible.

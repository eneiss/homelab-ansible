# Homelab Ansible Playbook

Playbook to configure several homelab VMs according to their use case.

## Required (non-versioned) files

Secret files. You will need to acquire them from someone who already has them.
- `secrets_file.enc`: Ansible variables file, encrypted by Ansible Vault.
- `password_file.pem`: Ansible Vault password file.
- `files/authorized_keys`: Authorized SSH keys file for your target hosts. **Will override any existing `~/.ssh/authorized_keys` file on your target hosts!**

Other files:
- `inventory/hosts`: Your inventory file.
Example content:
```ini
[test_vm]
192.168.1.23

[remote_proxy]
1.2.3.4 ansible_user=ubuntu ansible_ssh_private_key_file=~/.ssh/ansible
```

## Usage

- Create the required files mentioned above.
- Choose the YAML file you want to run between `main.yaml` and `reverse_proxy.yaml`.
- (Optional) Choose tags (`-t <tag-to-run>`) if you need to run only a specific role.
- Apply the playbook following the examples below:
```sh
# Run main playbook on 'my_host' 
ansible-playbook main.yaml -e @secrets_file.enc -e "variable_host=my_host"
# or for the reverse proxy
ansible-playbook reverse_proxy.yaml -e @secrets_file.enc -e "variable_host=reverse_proxy"
# only monitoring
ansible-playbook main.yaml -e @secrets_file.enc -t monitoring -e "variable_host=my_host"
# dry run (check)
ansible-playbook main.yaml -e @secrets_file.enc -e "variable_host=my_host" --check
```

## Notes

- Run `pip install passlib` to get rid of `[DEPRECATION WARNING]: Encryption using the Python crypt module is deprecated. [...]`
- Change the value of `packages_state` inside the main YAML to switch between lastest and present to update packages already installed or not.

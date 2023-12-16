# Homelab Ansible Playbook

Playbook to configure several homelab VMs according to their use case.

## Usage

- If needed, create the `inventory.ini` file at the root of the repo.
- Create the `secrets_file.enc` file and add its content that you should get from someone who already has it.
- Choose the YAML file you want to run between `mail.yml` and `reverse_proxy.yaml`.
- Update the host target of the YAML file.
- Choose tags (`-t tag-to-run`) if you need to run only a specific role.
- Apply the playbook following the examples below:
```sh
ansible-playbook main.yml -e @secrets_file.enc
# or for the reverse proxy
ansible-playbook reverse_proxy.yaml -e @secrets_file.enc
# only base
ansible-playbook main.yml -e @secrets_file.enc -t base
```

Notes:
- Run `pip install passlib` to get rid of `[DEPRECATION WARNING]: Encryption using the Python crypt module is deprecated. [...]`
- Change the value of `packages_state` inside the main YAML to switch between lastest and present to update packages already installed or not.

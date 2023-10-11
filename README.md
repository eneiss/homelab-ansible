```sh
ansible-playbook main.yml -e @secrets_file.enc
ansible-playbook reverse_proxy.yml -e @secrets_file.enc
```

Notes:
- `pip install passlib` to get rid of `[DEPRECATION WARNING]: Encryption using the Python crypt module is deprecated. [...]`
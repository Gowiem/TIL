# Stop Ansible from creating pesky playbook.retry files in ~/

Add a simple config flag in `~/.ansible.cfg`:

```
retry_files_enabled = False
```
Donalo [![CircleCI](https://circleci.com/gh/coopdevs/donalo.svg?style=svg)](https://circleci.com/gh/coopdevs/donalo)
=========

This repository provides the Ansible playbooks required to provision and deploy [Donalo's marketplace](https://github.com/coopdevs/sharetribe).

## Usage

### Provision

```
pyenv exec ansible-playbook playbooks/provision.yml --limit=production
```

Note these commands rely on the `vault_password_file` setting defined in [ansible.cfg](https://github.com/coopdevs/donalo/blob/08ed5c881901b053a6ea0e12ccc741d7cd1b321c/ansible.cfg#L5).

### Deploy

```
pyenv exec ansible-playbook playbooks/deploy.yml --limit=production
```

### Backups

Backups are done automatically every day at 03:45h with [backups_role](https://github.com/coopdevs/backups_role/) and stored in Blackblaze. To recover one run:

```
pyenv exec ansible-playbook playbooks/restore_backup.yml --limit=dev -K
```

## blog.donalo.org

This repository also handles redirects to this subdomain. Check out https://github.com/coopdevs/donalo/wiki/Old-blog-redirects for details.

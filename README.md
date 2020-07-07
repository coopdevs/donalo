Donalo [![CircleCI](https://circleci.com/gh/coopdevs/donalo.svg?style=svg)](https://circleci.com/gh/coopdevs/donalo)
=========

This repository provides the Ansible playbooks required to provision and deploy [Donalo's marketplace](https://github.com/coopdevs/sharetribe).

## Usage

### 1. Provision

```
pyenv exec ansible-playbook playbooks/provision.yml --limit=production
```

Note these commands rely on the `vault_password_file` setting defined in [ansible.cfg](https://github.com/coopdevs/donalo/blob/08ed5c881901b053a6ea0e12ccc741d7cd1b321c/ansible.cfg#L5).

### 2. Deploy

```
pyenv exec ansible-playbook playbooks/deploy.yml --limit=production
```

## blog.donalo.org

This repository also handles redirects to this subdomain. Check out https://github.com/coopdevs/donalo/wiki/Old-blog-redirects for details.

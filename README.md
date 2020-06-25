Donalo [![CircleCI](https://circleci.com/gh/coopdevs/donalo.svg?style=svg)](https://circleci.com/gh/coopdevs/donalo)
=========

## Migration from next.donalo.org to donalo.org

What follows are the steps that need to be performed to turn the current next.donalo.org server into the production one with the donalo.org domain pointing to it.

### Steps

#### 1. Change DNS record

First of all, for the provisioning to work and specifically the certificate, the DNS record `donalo.org` needs to point to 78.47.203.39. This needs to be asked to the DNS provider, Nexica.  This will cause downtime for the duration of the migration.

Once the DNS change is propagated, move on the next steps.

#### 2. Provision

```
pyenv exec ansible-playbook playbooks/provision.yml --limit=production
```

This will create a new database named `donalo` while keeping the existing `donalo_staging`. It will also change `RAILS_ENV` to `production`. However, the app won't switch to use these two until we restart Unicorn and Delayed Job.

The nginx site `donalo_https` will change its certificate and `server_name` to point to donalo.org failing to serve requests to `next.donalo.org`.

#### 3. Deploy

Once provisioned we'll need to deploy using the new inventory:

```
pyenv exec ansible-playbook playbooks/deploy.yml --limit=production
```

This will also restart the main services: Unicorn, Delayed Job and Sphinx making them pick the configuration provisioned in the step above.

Note these commands rely on the `vault_password_file` setting defined in [ansible.cfg](https://github.com/coopdevs/donalo/blob/08ed5c881901b053a6ea0e12ccc741d7cd1b321c/ansible.cfg#L5).

#### 4. blog.donalo.org

This subdomain is already pointing to the Wordpress site but only the admin can access it. We just need to make it public.

### To take into account

#### www and naked domain

There's a HTTP redirection done by the provider which redirects www.donalo.org to donalo.org , thus after changing the DNS record this should keep working. Now, donalo.org will resolve to 78.47.203.39 instead.

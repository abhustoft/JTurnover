# Nodejs

This will install Nodejs 0.10 or 0.12

## Requirements

None

## Role Variables

### Defaults

Default version to install is 0.10.

    nodejs_versjon: 0.10

You should override this in your `local.yml` to install 0.12. This
should only be installed for testing purposes for now. Nodejs 0.12
should not be used in production until we agree that it is stable.
We should also package it ourselves before installing it in
production.

## Gotchas

The 0.10 package does not include NPM, but 0.12 from nodesource does,
which is why you should conditionally include the NPM Ansible role based
on the Nodejs version you are using.

### Example

In your `meta/main.yml` given you are using this role to install Nodejs

  - role: npm
    when: nodejs_version == "0.10"

## Example Playbook

### Install 0.10

    - hosts: servers
      roles:
         - nodejs

### Install 0.12

The version would normally be overridden in `group_vars`.

    - hosts: servers
      roles:
        - { role: nodejs, nodejs_version: "0.12" }

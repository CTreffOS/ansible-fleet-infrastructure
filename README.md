# What is this?
This is a repository containing the Ansible configuration for the laptop-fleet of the [Chaostreff Osnabrück](https://chaostreff-osnabrueck.de).

# Adoption
As the very first step, you have to install your own key onto the machines (hopefully also part of the `authenticated_keys` for the playbook). Do that via:
```bash
ssh-copy-id user@ctreffosXX
```

## Preperation
```bash
. envsetup.source # to configure which inventory to use
ansible -m ping all # just to make you can reach them all
```

## Usage
```bash
ansible-playbook site.yml --ask-become-pass

# Contribution guidelines
* Never use `run_once: true`, because due to the strategy `free`, the task may be completed multiple times on different hosts, as they may start at different point of time.

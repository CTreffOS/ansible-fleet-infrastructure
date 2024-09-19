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

# Usage
```bash
ansible-playbook site.yml --ask-become-pass
```

## Block standby (during rollouts)
```bash
ansible-playbook power-block.yml --ask-become-pass
```

## Troubleshooting
The inventory is using the mDNS advertised hostnames of the machines. While this saves us from configureing the inventovry with fixed IPv4 addresses, it may lead to problems, if the mDNS/WiFi-connection is not working properly. I would recommend you to start with the `power-block.yml`-playbook and rerun it until all machines are reachable.

# Contribution guidelines
* Never use `run_once: true`, because due to the strategy `free`, the task may be completed multiple times on different hosts, as they may start at different point of time.
* Never use reboot or other power actions during a run - as `power-block.yml` will retrict them and may cause the playbook to get stuck.

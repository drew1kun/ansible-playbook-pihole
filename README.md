Ansible playbook: pihole
=========

[![MIT licensed][mit-badge]][mit-link]

Ansible playbook for automated [pihole][pihole-link] configuration

Does the following:

 - Bootstraps the pi using [drew-kun.bootstrap_core][bootstrap_core-galaxy-link] ansible role
 - Installs the [drew-kun.pihole][pihole-galaxy-link] ansible role
 - Installs the [drew-kun.dnscrypt][dnscrypt-galaxy-link] ansible role
 - Installs the [drew-kun.pitft][pitft-galaxy-link] ansible role

[drew-kun.pitft][pitft-galaxy-link] role installs the drivers for [Adafruit 28" tft Capacitive display][pitft-adafruit-link]

Requirements
------------

NOTE: Role requires Fact Gathering by ansible!

Playbook Variables
------------------

| Variable | Description | Default |
|----------|-------------|---------|
| **vault_bootstrap_core_new_root_passwd** | The encrypted root password in the form of randomly salted SHA512 hash | set your own in `vars/vault.yml`, please check [`drew-kun.bootstrap_core/default/main.yaml`][bc-root-passwd-link] for reference |
| **vault_bootstrap_core_users** | The list of users to be created on the system using the bootstrap_core role | set your own in `vars/vault.yml`, please check [`drew-kun.bootstrap_core/default/main.yaml`][bc-users-passwd-link] for reference |
| **vault_bootstrap_core__rpi3_network_wifi_APs** | The list of wifi networks to be configured on the system using the rpi3_network role | set your own in `vars/vault.yml`, please check [`drew-kun.rpi3_network/default/main.yaml`][net-aps-link] for reference |
| **vault_pitft_pi_passwd** | The encrypted pi user password in the form of randomly salted SHA512 hash | set your own in `vars/vault.yml`, please check [`drew-kun.pitft/default/main.yaml`][pitft-pi-passwd-link] for reference |
| **vault_pihole_setupVars_conf_WEBPASSWD** | Password for pihole web interface for quiet `pihole` installation | see [`drew-kun.pihole/default/main.yaml`][pihole-web-passwd-link] |


Dependencies
------------
Roles:
 - [drew-kun.bootstrap_core][bootstrap_core-galaxy-link] ansible role
 - [drew-kun.pihole][pihole-galaxy-link] ansible role
 - [drew-kun.dnscrypt][dnscrypt-galaxy-link] ansible role
 - [drew-kun.pitft][pitft-galaxy-link] ansible role

Install via ansible-galaxy:

    ansible-galaxy install drew-kun.bootstrap_core \
                           drew-kun.pihole \
                           drew-kun.dnscrypt \
                           drew-kun.pitft

Playbook Usage Example
----------------------

**ATTENTION!**

variables are set in **vars/vault.yml**,
which is encrypted with [ansible-vault][ansible-vault-link].

Therefore we have multiple options to run the play:

### OPTION 0:
Just put the `.vault.key` to the playbook dir and run play:

    ansible-playbook --user user -k pihole_playbook.yml --vault-password-file=.vault.key

### OPTION 1:
Before running the role decrypt the file *vars/main.yml* with:

    ansible-vault decrypt vars/main.yml --vault-password-file=.vault.key`

Then run play:

    ansible-playbook --user user -k pihole_playbook.yml

### OPTION 2:
Set environment variable:

    export ANSIBLE_VAULT_PASSWORD_FILE=.vault.key

Then run play:

    ansible-playbook --user user -k pihole_playbook.yml

### OPTION 3 (PREFERRED):
add the following to **ansible.cfg**:

    [defaults]
    vault_password_file = .vault.key

Modify the **vars/vault.yml** as you wish using:

    ansible-vault edit vars/vault.yml

Then run play as follows:

    ansible-playbook --user user -k pihole_playbook.yml

License
-------

[MIT][mit-link]

Author Information
------------------

Andrew Shagayev | [e-mail](mailto:drewshg@gmail.com)

[pihole-link]: https://pi-hole.net
[ansible-vault-link]: https://docs.ansible.com/ansible/latest/user_guide/vault.html
[bootstrap_core-galaxy-link]: https://galaxy.ansible.com/drew-kun/bootstrap_core/
[pihole-galaxy-link]: https://galaxy.ansible.com/drew-kun/pihole/
[dnscrypt-galaxy-link]: https://galaxy.ansible.com/drew-kun/dnscrypt/
[pitft-galaxy-link]: https://galaxy.ansible.com/drew-kun/pitft/
[pitft-adafruit-link]: https://www.adafruit.com/product/2423
[pitft-pi-passwd-link]: https://github.com/drew-kun/ansible-pitft/blob/master/defaults/main.yml#L24
[pihole-web-passwd-link]: https://github.com/drew-kun/ansible-pihole/blob/master/defaults/main.yml#L17
[bc-root-passwd-link]: https://github.com/drew-kun/ansible-bootstrap_core/blob/master/defaults/main.yml#L24
[bc-users-passwd-link]: https://github.com/drew-kun/ansible-bootstrap_core/blob/master/defaults/main.yml#L29
[net-aps-link]: https://github.com/drew-kun/ansible-rpi3_network/blob/master/defaults/main.yml#L20


[mit-badge]: https://img.shields.io/badge/license-MIT-blue.svg
[mit-link]: https://raw.githubusercontent.com/drew-kun/ansible-macos_setup/master/LICENSE

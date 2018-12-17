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
| **vault_pitft_pi_passwd** | The encrypted pi user password in the form of randomly salted SHA512 hash | set your own in `vars/vault.yml`, please check [drew-kun.pitft][pitft-galaxy-link] (`default/main.yml#L22`) for reference |
| **vault_pihole_setupVars_conf_WEBPASSWD** | Password for pihole web interface for quiet `pihole` installation | see [`vars/vault.yml`(vars/vault.yml#L35) |

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

**vault_pihole_setupVars_conf_WEBPASSWD** var is set in *vars/vault.yml*,
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

Then run play as follows:

    ansible-playbook --user user -k pihole_playbook.yml

License
-------

[MIT][mit-link]

Author Information
------------------

Andrew Shagayev | [e-mail](mailto:drewshg@gmail.com)

[pihole-link]: https://pi-hole.net

[bootstrap_core-galaxy-link]: https://galaxy.ansible.com/drew-kun/bootstrap_core/
[pihole-galaxy-link]: https://galaxy.ansible.com/drew-kun/pihole/
[dnscrypt-galaxy-link]: https://galaxy.ansible.com/drew-kun/dnscrypt/
[pitft-galaxy-link]: https://galaxy.ansible.com/drew-kun/pitft/
[pitft-adafruit-link]: https://www.adafruit.com/product/2423

[mit-badge]: https://img.shields.io/badge/license-MIT-blue.svg
[mit-link]: https://raw.githubusercontent.com/drew-kun/ansible-macos_setup/master/LICENSE

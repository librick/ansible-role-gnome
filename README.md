# Ansible Role: GNOME Desktop Environment
[![pre-commit](https://img.shields.io/badge/pre--commit-enabled-brightgreen?logo=pre-commit)](https://github.com/pre-commit/pre-commit)

This role installs and customizes the GNOME desktop environment on Debian-based Linux systems. It:
 - Ensures that GNOME session manager is installed
 - Ensures that GNOME-related apt packages are installed
 - Ensures that *undesired* GNOME-related apt packages are *not* installed
 - Sets common GNOME settings via the GSettings API and dconf

## Role Variables
See `defaults/main.yml` for a comprehensive list of role variables.  
Some of the most pertinent variables are:
- `gnome_user`
- `gnome_xdg_config_home`
- `gnome_apt_packages_to_install`
- `gnome_apt_packages_to_remove`
- `gnome_dash_apps`

## Dependencies
Uses `psutil` python3 package for use by the `community.general.dconf` module.  
On Debian, `psutil` can be installed via apt package: `python3-psutil`.  
See the docs for the [Ansible community.general.dconf module](https://docs.ansible.com/ansible/latest/collections/community/general/dconf_module.html)

## Testing
Testing is performed using Molecule.  
See the [molecule](./molecule/) directory for more information.

## Linting
Linting is done automatically via [https://pre-commit.com/](https://pre-commit.com/).  
After setting up a virtual environment and installing `requirements.txt`, run  
`pre-commit run --all-files`  
See: https://github.com/ansible/ansible-lint  
See: https://github.com/pre-commit/pre-commit

## Example Playbook
    - hosts: servers
      vars_files:
        - vars/main.yml
      roles:
        - librick.gnome

*Inside `vars/main.yml`*:

    gnome_user: johndoe
    gnome_gsettings_disable_caps_lock: false
    gnome_gsettings_disable_animation: false
    gnome_apt_packages_to_install:
      - gnome-shell
      - gnome-calculator

## License

MIT Licensed

## Author Information

This role was created in 2023 by [Eric McDonald](https://juniperspring.xyz/).

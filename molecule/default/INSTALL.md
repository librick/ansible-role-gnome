## Running Tests
This role uses Molecule and Vagrant for integration testing.  
Install the Vagrant CLI on Debian:  

    wget -O- https://apt.releases.hashicorp.com/gpg | gpg --dearmor | sudo tee /usr/share/keyrings/hashicorp-archive-keyring.gpg`  
    echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list`  
    sudo apt update && sudo apt install vagrant` 
 
Enable autocomplete for Vagrant CLI (optional but recommended); you may need to reload your terminal emulator after this command for it to take effect:  
`vagrant autocomplete install --bash --zsh`  
Verify that the Vagrant CLI is installed:  
`vagrant --version`

Molecule support for Vagrant is provided via a plugin.
See: https://github.com/ansible-community/molecule-plugins

Set up a virtual environment with `venv`:  
`python3 -m venv venv`  
Activate the environment:  
`source ./venv/bin/activate`  
Ensure ansible packages are managed by pip3 venv rather than apt:  
`sudo apt-get purge ansible ansible-core ansible-lint`  
Ensure that `pip3` binary is `.../venv/bin/pip3`:  
`which pip3`  
Ensure old-style molecule plugins are not installed  
See: https://github.com/ansible-community/molecule-plugins  
`pip3 uninstall molecule-docker molecule-vagrant`  
Install python3 packages, including ansible, molecule, and linting tools:  
`pip3 install -r requirements.txt`  
Ensure ansible is latest version:  
`pip3 install --upgrade ansible`  
Install community.general modules:  
`ansible-galaxy collection install community.general`  
Ensure $USER is in the libvirt group  
This is optional but avoids the developer being spammed with UAC prompts  
Be aware that this has security implications!  
`sudo usermod -a -G libvirt user`

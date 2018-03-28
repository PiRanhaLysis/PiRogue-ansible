# Ansible playbook for the PiRogue

The following steps must be conducted on a computer which will remotely install the PiRogue customization on your fresh Kali GNU/Linux install. 

## How to use the playbook
### Install ansible
To install ansible, please follow the [Ansible documentation guide](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html).

### Add the IP address of you PiRogue
Edit the file `inventory.ini` and correct the IP address specified just after `ansible_host=`. It should look like:
```
pirogue_1 ansible_host=192.168.1.123  ansible_ssh_user=root
```

### Run the playbook
Simply run the following command: 
```
ansible-playbook -i inventory.ini --ask-pass pirogue.yml
```
It will ask you an SSH password, use `toor` if you do not have changed your password on your PiRogue, otherwise, use your new password.
# Ansible playbook for the PiRogue

Ansible is a tool that allows you to setup easily computers. As a PiRogue is a computer and as we want its setup the easiest as possible,

## Before starting

Any Raspberry pi from v2 to v3B+ should work.

You will need to flash a raspbian-lite image on your sdcard.

You can download raspbian from https://www.raspberrypi.org/downloads/raspbian/

Then follow the setup guide here : https://www.raspberrypi.org/documentation/installation/installing-images/README.md

Once raspbian is installed (you can login with pi/raspberry), we should do two things:

* configure keyboard disposition
* change pi password
* change root password
* enable ssh (Ansible will use ssh to setup your pi)
* get you raspberrypi IP address

### configure keyboard disposition

type ```sudo raspi-config```:


```bash
pi@raspberry$ sudo raspi-config
```

Then choose ```Localisation Options``` and ```Change Keyboard Layout```

Configure your keyboard then exit raspi-config


### change pi password

type ```passwd``` command:

```bash
pi@raspberry$ passwd
```

enter a new password and its confirmation

### change root password

type ```sudo passwd root``` command:

```bash
pi@raspberry$ sudo passwd root
```

enter a new password and its confirmation

### enable ssh

type ```sudo raspi-config```:


```bash
pi@raspberry$ sudo raspi-config
```

Choose ```Interfacing Options``` then ```SSH```, answer ```yes``` to "Would you like the SSH server to be enabled?" question.

### Get your raspberrypi IP address

Connect your raspberrypi with a network wire to your internet router.

then type the following command on your pi:

```bash
pi@raspberry$ ip a s dev eth0 | grep inet

    inet 192.168.1.20/24 brd 192.168.1.255 scope global eth0
    inet6 fe80::ba27:ebff:feeb:4f08/64 scope link

```

Here, our raspberrypi has 192.168.1.20 IP address. You must remember this address has we will use it to tell Ansible which computer it must PiRogue tools on.

# Installing PiRogue tools

The following steps must be conducted on a computer which will remotely install the PiRogue customization on your fresh Kali GNU/Linux install. 

## How to use the playbook
### Install ansible
To install ansible, please follow the [Ansible documentation guide](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html).

### Add the IP address of you PiRogue
Edit the file `inventory.ini` and correct the IP address (the one you got at *Get your raspberrypi IP address* section of this readme file) specified just after `ansible_host=`. It should look like:

```
pirogue_1 ansible_host=192.168.1.20  ansible_ssh_user=root
```

### Configure your PiRogue

Edit *roles/pirogue/defaults/main.yml* to match you requirements passwords, wifi settings, ...

### Run the playbook
Simply run the following command: 
```
ansible-playbook -i inventory.ini --become --ask-become-pass --ask-pass --diff pirogue.yml
```
It will ask you an SSH password, use `toor` if you do not have changed your password on your PiRogue, otherwise, use your new password.

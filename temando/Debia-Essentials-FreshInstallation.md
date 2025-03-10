[Go Back](https://rmelendez.net)

## Essential Packages
One liner *(I will try to make a bash script later)*
```bash
sudo apt install zsh git curl
```

## Debian Server Fresh Installation Possible Issues
**Error/Issue** - `sudo: command not found` 
**Description** - Unable to install package by using `sudo`
**Solution** - Install `sudo` by running `su -` then `apt install sudo`

Assuming that you added a `root passwd` the user the installation asks you to create will not be in the `sudo` group, to fix it, do the following
```bash
su - # This will put you as root, it will also ask you for the root passwd

apt install sudo # Install sudo package

adduser username sudo # Adds user to sudo group

reboot # You might need to reboot the server
```

**Error/Issue** - `name_of_host name or service not known`
**Description** - Unable to add `/etc/apt/keyrings` when attempting to install `docker`
**Solution** - Add `hostname` to `/etc/hosts` usually it is the 3rd line. Both `hostname` and `/etc/hosts` needs to match
A Modded Bash script for managing proot'ed Linux distributions in Termux. Addition of Ubuntu 21.04.
Please Uninstall existing proot-distro using "pkg uninstall proot-distro"

For now it supports installation of these distributions:

* Alpine Linux
* Arch Linux / Arch Linux ARM
* Debian Buster
* Fedora 33
* Kali Nethunter (rootless)
* Parrot OS (LTS)
* Ubuntu (18.04 / 20.04 / 21.04)

## Usage example

Install package in Termux:
```
pkg update -y && pkg upgrade -y
pkg install git wget -y
git clone git://github.com/srivathsarao/proot-distro.git
cd proot-distro
./install.sh
```

Example on how to install Ubuntu and launch shell:
```
proot-distro install ubuntu-20.04
proot-distro login ubuntu-20.04
```

You may create a distribution installation with custom name:
```
proot-distro install --override-alias ubuntu-testing ubuntu-20.04
proot-distro login ubuntu-testing
```
This will allow to have multiple installations of same distribution.

## Fixing dpkg errors

1. udisks2
   ```
   dpkg: error processing package udisks2 (--configure):
    installed udisks2 package post-installation script subprocess returned error exit status 1
   ```
   Solution:
   ```
   rm /var/lib/dpkg/info/udisks2.postinst
   dpkg --configure -a
   ```
2. libfprint-2-2
   ```
   dpkg: error processing package libfprint-2-2:arm64 (--configure):
    installed libfprint-2-2:arm64 package post-installation script subprocess returned error exit status 1
   ```
   Solution:
   ```
   rm /var/lib/dpkg/info/libfprint0:*.postinst
   dpkg --configure -a
   ```
3. fprintd
   ```
   rm /var/lib/dpkg/info/fprintd.postinst
   dpkg --configure -a
   ```

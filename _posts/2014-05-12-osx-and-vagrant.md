---
layout: single
title:  "OSX and Vagrant!"
tags:
  - vagrant
  - osx
redirect_from:
  - /2014/05/12/osx-and-vagrant/
  - /osx-and-vagrant/
  - /vagrant/osx/2014/05/12/osx-and-vagrant.html
---

So whilst trying to get [boxen](http://boxen.github.com/) to work I needed a good method to test, so of course I turned to [Vagrant](http://www.vagrantup.com/) and standing on the works of others (namely [Graham Gilbert](http://grahamgilbert.com/blog/2013/08/23/creating-an-os-x-base-box-for-vagrant-with-packer/) ) I used the following steps:

Requirements
---------

* [Packer](http://packer.io/downloads.html)
* [Vagrant](http://www.vagrantup.com/)
* [VMware Fusion](http://www.vmware.com/uk/products/fusion)

Steps
----

Download and install packer, the easiest method to do this I found was using [homebrew](http://brew.sh/)

```bash
$ brew install packer
Cloning into '/opt/boxen/homebrew/Library/Taps/homebrew/homebrew-binary'...
remote: Reusing existing pack: 143, done.
remote: Total 143 (delta 0), reused 0 (delta 0)
Receiving objects: 100% (143/143), 22.89 KiB | 0 bytes/s, done.
Resolving deltas: 100% (66/66), done.
Checking connectivity... done.
Tapped 13 formula
==> Downloading https://dl.bintray.com/mitchellh/packer/0.6.0_darwin_amd64.zip
######################################################################## 100.0%
🍺  /opt/boxen/homebrew/Cellar/packer/0.6.0: 33 files, 377M, built in 11.9 minutes
```
Get the OSX template for packer

```bash
$ mkdir $HOME/tmp && cd $HOME/tmp
$ git clone https://github.com/timsutton/osx-vm-templates.git
Cloning into 'osx-vm-templates'...
remote: Reusing existing pack: 193, done.
remote: Total 193 (delta 0), reused 0 (delta 0)
Receiving objects: 100% (193/193), 98.27 KiB | 0 bytes/s, done.
Resolving deltas: 100% (77/77), done.
Checking connectivity... done.
```

Prepare packer to install Mavericks

```bash
$ cd $HOME/tmp/osx-vm-templates
$ sudo prepare_iso/prepare_iso.sh "/Applications/Install OS X Mavericks.app" out
```
This should result in :

```bash
$HOME/tmp/osx-vm-templates/out/OSX_InstallESD_10.9.2_13C64.dmg
-- Fixing permissions..
-- Checksumming output image..
-- MD5: dbe60cbeab09208e3ed20985975068b9
-- Done. Built image is located at out/OSX_InstallESD_10.9.2_13C64.dmg. Add this iso and its checksum to your template.
```
Then change packer/template.json to insert the DMG source and checksum

```bash
$ cd packer/ && packer build template.json
```
And once that has done it's thing you will end up with :

```bash
$ vagrant box add osx packer_vmware-iso_vmware.box
==> box: Adding box 'osx' (v0) for provider:
    box: Downloading: file://.../packer/packer_vmware-iso_vmware.box
==> box: Successfully added box 'osx' (v0) for 'vmware_desktop'!
```

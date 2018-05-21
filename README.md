
# GovTechStack.sg Centos Training VM

This is a Packer script to build a Centos 7 Desktop image for use in GovTechStack.sg training sessions.

Pushed to vagrant cloud as govtechstacksg/centos

# Prerequisites

 - Vagrant
 - VirtualBox

**Vagrant download link**

    https://www.vagrantup.com/downloads.html

**VirtualBox download link**

    https://www.virtualbox.org/wiki/Downloads

# Creating the Vagrantfile

    touch Vagrantfile

# Running the Vagrant image

Copy the following text to a file  ```Vagrantfile```
```ruby
# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "govtechstacksg/centos"

  # Forwarded Ports
  config.vm.network "forwarded_port", guest: 22, host: 22
  config.vm.network "forwarded_port", guest: 3000, host: 3000
  config.vm.network "forwarded_port", guest: 8080, host: 8080
  config.vm.network "forwarded_port", guest: 8443, host: 8443
  config.vm.network "forwarded_port", guest: 80, host: 80
  config.vm.network "forwarded_port", guest: 443, host: 443

  # Configure and optimize according to your system specs
  config.vm.provider "virtualbox" do |vb|
    vb.gui = true
    vb.cpus = 2
    vb.memory = "4096"
    vb.customize ["modifyvm", :id, "--clipboard", "bidirectional"]
    vb.customize ["modifyvm", :id, "--draganddrop", "bidirectional"]
    vb.customize ["modifyvm", :id, "--usbxhci", "on"]
  end


  # config.vm.provision "shell", inline: <<-SHELL
  #   sudo yum install -y your-package-here
  # SHELL
end
```

Run the command:

```bash
vagrant up
```

> If you have a previous image already built, run the following commands to remove them. Then run ```vagrant up```
```bash
vagrant destroy --force
vagrant box remove govtechstacksg/centos
```

As per Vagrant box conventions, the credentials to use the image are as follows:
```
Username: vagrant
Password: vagrant
```
# Possible Errors

    

`Stderr: VBoxManage: error: Implementation of the USB 3.0 controller not found!`

To fix this problem, either install the 'Oracle VM VirtualBox Extension Pack' or disable USB 3.0 support in the VM settings

-   [Oracle VM VirtualBox Extension Pack](https://download.virtualbox.org/virtualbox/5.2.12/Oracle_VM_VirtualBox_Extension_Pack-5.2.12.vbox-extpack)


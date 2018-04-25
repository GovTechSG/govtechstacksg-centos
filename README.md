# GovTechStack.sg Centos Training VM

This is a Packer script to build a Centos 7 Desktop image for use in GovTechStack.sg training sessions.

Pushed to vagrant cloud as govtechstacksg/centos


# Running the Vagrant image

Copy the following text to a file named ```Vagrantfile```
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
  end


  # config.vm.provision "shell", inline: <<-SHELL
  #   sudo yum install -y your-package-here
  # SHELL
end
```

Run the following commands:
```bash
vagrant destroy --force
vagrant box remove govtechstacksg/centos
vagrant up
```

As per Vagrant box conventions, the credentials to use the image are as follows:
Username: vagrant
Password: vagrant

# -*- mode: ruby -*-
# vi: set ft=ruby :
# This is a Vagrant configuration file. It can be used to set up and manage
# virtual machines on your local system or in the cloud. See http://downloads.vagrantup.com/
# for downloads and installation instructions, and see http://docs.vagrantup.com/v2/
# for more information and configuring and using Vagrant.

Vagrant.configure("2") do |config|

  config.vm.box = "hashicorp/precise64"

  config.vm.hostname = "vrologist-com"

  # If you have problems start your Vagrant VM then you can comment out both of these lines,
  # but "jekyll serve --watch" might not detect changes to files.
  # config.vm.network "private_network", type: "dhcp"
  # config.vm.synced_folder ".", "/vagrant", type: "nfs", mount_options: ['actimeo=1']

  config.vm.network :forwarded_port, guest: 3000, host: 7777, auto_correct: true

  # increases the processing capacity
  # Ram 4096
  # Processors 4
  config.vm.provider :virtualbox do |vb|
    # Use VBoxManage to customize the VM.
    vb.customize ["modifyvm", :id, "--memory", "4096"]
    vb.customize ["modifyvm", :id, "--cpus", "4"]
  end

  # Update apt-get
  config.vm.provision :shell, :inline => "sudo apt-get update --fix-missing"

  # Ruby / Rubygems / Bundler
  config.vm.provision :shell, :inline => "sudo apt-get -y install curl"
  config.vm.provision :shell, :path => "vagrant/install-rvm.sh",  :args => "stable"
  config.vm.provision :shell, :path => "vagrant/install-ruby.sh", :args => "2.2"
  config.vm.provision :shell, :inline => "rvm rvmrc trust /vagrant"
  config.vm.provision :shell,
    :inline => "sudo apt-get install -y rubygems"
  config.vm.provision :shell, :inline => "cd /vagrant; rvm 2.2 do gem install bundler"

  # Gem bundle
  config.vm.provision :shell, :privileged => false,
    :inline => "cd /vagrant; rvm 2.2 do bundle install"

  # Node.js
  config.vm.provision :shell,
    :inline => "apt-get install -y python-software-properties python g++ make"
  config.vm.provision :shell,
    :inline => "add-apt-repository ppa:chris-lea/node.js"
  config.vm.provision :shell, :inline => "sudo apt-get update"
  config.vm.provision :shell, :inline => "sudo apt-get install -y nodejs"

end

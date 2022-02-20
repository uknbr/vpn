# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # Box
  config.vm.box = "bento/ubuntu-18.04"
  config.vm.box_download_insecure=true

  # VM settings
  config.vm.provider "virtualbox" do |vbox|
    vbox.name = "vpn"
    vbox.memory = 1024
    vbox.cpus = 1
    vbox.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    vbox.customize ["modifyvm", :id, "--ioapic", "on"]
    vbox.customize ["modifyvm", :id, "--name", "vpn"]
  end

  # Share
  config.vm.synced_folder '.', '/vagrant', SharedFoldersEnableSymlinksCreate: false

  # Network | NAT - Forward ports
  config.vm.network :forwarded_port, guest: 1194, host: 1194

  # VM name
  config.vm.define :vpn do |vpn|
  end
  config.vm.hostname = "vpn"

end
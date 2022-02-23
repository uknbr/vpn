# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"
HOST_IP = ENV["WINDOWS_STATIC_IP"]

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # Box
  config.vm.box = "bento/ubuntu-20.04"
  config.vm.box_download_insecure=true

  # VM settings
  config.vm.provider "virtualbox" do |vbox|
    vbox.name = "vpn"
    vbox.memory = 1536
    vbox.cpus = 2
    vbox.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    vbox.customize ["modifyvm", :id, "--ioapic", "on"]
    vbox.customize ["modifyvm", :id, "--name", "vpn"]
  end

  # Share
  config.vm.synced_folder '.', '/vagrant', SharedFoldersEnableSymlinksCreate: false

  # Network | NAT - Forward ports
  config.vm.network :forwarded_port, guest: 1194, host: 1194
  config.vm.network :forwarded_port, id: "ssh_wsl2_ip", guest: 22, host_ip: HOST_IP, host: 2222

  # VM name
  config.vm.define :vpn do |vpn|
  end
  config.vm.hostname = "vpn"

  # Run Ansible - Locally
  config.vm.provision "ansible_local" do |ansible|
    ansible.playbook = "./setup/vpn.yaml"
    ansible.install = true
    ansible.config_file = "./setup/ansible.cfg"
    ansible.verbose = "vvv"
    ansible.skip_tags = ["ssh", "update"]
    ansible.extra_vars = {
      vpn_name: "vagrant",
      vpn_password: "vagrant"
    }
  end

end
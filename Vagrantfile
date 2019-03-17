# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "debian/contrib-stretch64"

  config.vm.provider "virtualbox" do |vb|
    # Customize the amount of memory on the VM:
    vb.memory = "2048"
    vb.cpus = 4
  end

  (1..3).each do |i|
    config.vm.define "default-#{i}" do |node|
      node.vm.network "private_network", ip: "192.168.50.10#{i}"
    end
  end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "playbook.yml"
    ansible.groups = {
      "vpn": ["default-1", "default-2", "default-3"],
    }
  end
end

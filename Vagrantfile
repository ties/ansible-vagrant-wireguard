# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  # config.vm.box = "debian/contrib-stretch64"
  config.vm.box = "debian/buster64"


  config.vm.provider "virtualbox" do |vb|
    vb.memory = "2048"
    vb.cpus = 4
  end

  config.vm.provider :libvirt do |libvirt|
    # system session - create network
    libvirt.qemu_use_session = false
    libvirt.system_uri = 'qemu:///system'

    libvirt.cpus = 4
    libvirt.memory = "2048"
  end

  (1..3).each do |i|
    config.vm.define "default-#{i}" do |node|
      # node.vm.synced_folder './', '/vagrant'
      # , type: '9p', disabled: false, accessmode: "squash"
      config.vm.synced_folder ".", "/vagrant", disabled: true
      node.vm.network :private_network,
                      :type => "dhcp",
                      :libvirt__network_name => "vagrant_wireguard_private",
                      :libvirt__network_address => "192.168.50.10#{i}"
    end
  end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "playbook.yml"
    ansible.groups = {
      "vpn": ["default-1", "default-2", "default-3"],
    }
  end
end

# -*- mode: ruby -*-
# vim: set ft=ruby :
GLOBAL_VARS ={}
MACHINES = {
  :inetRouter => {
    :box_name => "almalinux/9",
    :net => [
      {adapter: 2, auto_config: false, virtualbox__intnet: "router-net"},
      {adapter: 3, auto_config: false, virtualbox__intnet: "router-net"},
      {ip: '192.168.56.10', adapter: 8},
    ],
    :vars => {}
  },
  :centralRouter => {
    :box_name => "almalinux/9",
    :net => [
      {adapter: 2, auto_config: false, virtualbox__intnet: "router-net"},
      {adapter: 3, auto_config: false, virtualbox__intnet: "router-net"},
      {ip: '192.168.255.9', adapter: 6, netmask: "255.255.255.252", virtualbox__intnet: "office1-central"},
      {ip: '192.168.56.11', adapter: 8},
    ],
    :vars => {}
  },

  :office1Router => {
    :box_name => "almalinux/9",
    :net => [
      {ip: '192.168.255.10', adapter: 2, netmask: "255.255.255.252", virtualbox__intnet: "office1-central"},
      {adapter: 3, auto_config: false, virtualbox__intnet: "vlan1"},
      {adapter: 4, auto_config: false, virtualbox__intnet: "vlan1"},
      {adapter: 5, auto_config: false, virtualbox__intnet: "vlan2"},
      {adapter: 6, auto_config: false, virtualbox__intnet: "vlan2"},
      {ip: '192.168.56.20', adapter: 8},
    ],
    :vars => {}
  },

  :testClient1 => {
    :box_name => "almalinux/9",
    :net => [
      {adapter: 2, auto_config: false, virtualbox__intnet: "testLAN"},
      {ip: '192.168.56.21', adapter: 8},
    ],
    :vars => {}
  },

  :testServer1 => {
    :box_name => "almalinux/9",
    :net => [
      {adapter: 2, auto_config: false, virtualbox__intnet: "testLAN"},
      {ip: '192.168.56.22', adapter: 8},
    ],
    :vars => {}
  },

  :testClient2 => {
    :box_name => "ubuntu/jammy64",
    :net => [
      {adapter: 2, auto_config: false, virtualbox__intnet: "testLAN"},
      {ip: '192.168.56.31', adapter: 8},
    ],
    :vars => {}
  },

  :testServer2 => {
    :box_name => "ubuntu/jammy64",
    :net => [
      {adapter: 2, auto_config: false, virtualbox__intnet: "testLAN"},
      {ip: '192.168.56.32', adapter: 8},
    ],
    :vars => {}
  },

}

Vagrant.configure("2") do |config|
  config.vm.box_check_update = false
  config.vm.provider :virtualbox
  config.vm.provider "virtualbox" do |vb|
    vb.customize [ "modifyvm", :id, "--uartmode1", "disconnected" ]
  end
  MACHINES.each do |boxname, boxconfig|
    config.vm.define boxname do |box|
      box.vm.box = boxconfig[:box_name]
      box.vm.host_name = boxname.to_s
      boxconfig[:net].each do |ipconf|
        box.vm.network "private_network", **ipconf
      end
      box.vm.provision "ansible" do |ansible|
        ansible.compatibility_mode = "2.0"
        ansible.playbook = "ansible/playbook.yml"
        ansible.extra_vars = GLOBAL_VARS.merge(boxconfig[:vars]).merge({host_name: boxname.to_s})
        ansible.host_key_checking = "false"
        ansible.become = "true"
        ansible.limit = "all"
      end
    end
  end
end

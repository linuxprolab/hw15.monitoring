# -*- mode: ruby -*-
# vim: set ft=ruby :

MACHINES = {
  :'system' => {
    :host_name => 'system',
    :box_name => "centos/8",
    :net => [
      {ip: '192.168.0.1', adapter: 2, netmask: "255.255.255.0", virtualbox__intnet: "internal-net"},           
    ],
    :ports => [
      {guest: 22, host: 22001, id: 'ssh'}, 
    ], 
    :memory => 4096,
    :cpus => 2,
  },
  :'monitoring' => {
    :host_name => 'monitoring',
    :box_name => "centos/8",
    :net => [
      {ip: '192.168.0.2', adapter: 2, netmask: "255.255.255.0", virtualbox__intnet: "internal-net"},           
    ],
    :ports => [
      {guest: 22, host: 22002, id: 'ssh'}, 
      {guest: 9090, host: 9090}, 
      {guest: 3000, host: 3000},
    ],
    :memory => 4096,
    :cpus => 2,
  },
}

Vagrant.configure("2") do |config|

  MACHINES.each do |boxname, boxconfig|

    config.vm.define boxname do |box|
      box.vm.synced_folder ".", "/vagrant", type: "rsync", disabled: true
      box.vm.box = boxconfig[:box_name]
      box.vm.host_name = boxname.to_s

      if boxconfig.key?(:public)
         box.vm.network "public_network", boxconfig[:public]
      end

      boxconfig[:net].each do |ipconf|
        box.vm.network "private_network", ipconf
      end
      if boxconfig[:ports]
        boxconfig[:ports].each do |portconf|
          box.vm.network "forwarded_port", portconf
        end
      end 
      if boxconfig[:memory]
        box.vm.provider "virtualbox" do |v|
          v.memory = boxconfig[:memory]
          #v.cpus = box[:cpus]
        end
      end 
     # box.vm.provision "ansible" do |ansible|
     #   ansible.playbook = "provisioning/main.yml"
      #end
    end
  end
end


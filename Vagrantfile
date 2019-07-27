  
# -*- mode: ruby -*-
# vim: set ft=ruby :

MACHINES = {
  :"mon" => {
    :box_name => "centos/7",
    :ip_addr => "172.20.10.50",
    :memory => "1024",
    :shell => "mon.sh",
    :ansible => "site.yml"
  }
}

Vagrant.configure("2") do |config|

  MACHINES.each do |boxname, boxconfig|

    config.vm.define boxname do |box|
      box.vm.box = boxconfig[:box_name]
      box.vm.host_name = boxname.to_s
      box.vm.network "private_network", ip: boxconfig[:ip_addr]
      box.vm.provider "virtualbox" do |v|
        v.name = boxname.to_s
        v.memory = boxconfig[:memory]
      box.vm.provision "shell", path: boxconfig[:shell]
        end
        box.vm.provision "ansible_local" do |ansible|
        ansible.playbook = boxconfig[:ansible]
        end
    end
  end
end
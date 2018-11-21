# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.synced_folder ".", "/vagrant", disabled: false

  config.vm.define "master" do |master|
    master.vm.box = "ubuntu/xenial64"
    master.vm.provider "virtualbox" do |v|
      v.memory = 4096
      v.cpus = 1	  
    end  
	
	master.vm.network "private_network", ip: "192.168.66.100", virtualbox__intnet: true	
  
    master.vm.network "forwarded_port", guest: 443, host: 4001, id: "master_https"
	
	master.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "playbook_master.yml"
	end     	
  end
  
  config.vm.define "slave" do |slave|    
  
    slave.vm.box = "ubuntu/xenial64"
    slave.vm.provider "virtualbox" do |v|
      v.memory = 4096
      v.cpus = 2
    end  
	
	slave.vm.network "private_network", ip: "192.168.66.200", virtualbox__intnet: true	
  
	slave.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "playbook_slave.yml"
    end
  end
  
end

# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.ssh.insert_key = false
  config.vm.define "stage" do |stage|
    stage.vm.box = "geerlingguy/ubuntu1404"
    stage.vm.hostname = 'stage.local'
    stage.vm.box_url = "ubuntu/precise64"

    stage.vm.network :private_network, ip: "192.168.33.2"

    stage.vm.provider :virtualbox do |v|
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--memory", 512]
      v.customize ["modifyvm", :id, "--name", "stage"]
    end
  end

  config.vm.define "production" do |production|
    production.vm.box = "geerlingguy/ubuntu1404"
    production.vm.hostname = 'production.local'
    production.vm.box_url = "ubuntu/precise64"

    production.vm.network :private_network, ip: "192.168.33.3"

    production.vm.provider :virtualbox do |v|
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--memory", 512]
      v.customize ["modifyvm", :id, "--name", "production"]
    end
#  end
#end


  # Ansible provisioner.
  config.vm.provision "ansible" do |ansible|
    ansible.verbose = "v"
    ansible.limit = "all"
    ansible.playbook = "provisioning/playbook.yml"
    ansible.inventory_path = "provisioning/inventory"
    ansible.sudo = true
  end
end
end

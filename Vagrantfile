# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "bento/amazonlinux-2"

  config.vm.define "wordpress" do |app|
    app.vm.network :private_network, ip: "192.168.33.10"
    app.vm.network "forwarded_port", guest: 80, host: 8080
    app.vm.provision "ansible_local" do |ansible|
      ansible.become = true
      ansible.playbook = "app.yml"
      ansible.install_mode = "pip"
      ansible.version = "2.9.3"
      ansible.inventory_path = "inventories/local/hosts"
      ansible.limit = "all"
    end
  end

  config.vm.define "database" do |db|
    db.vm.network :private_network, ip: "192.168.33.20"
    db.vm.provision "ansible_local" do |ansible|
      ansible.become = true
      ansible.playbook = "db.yml"
      ansible.install_mode = "pip"
      ansible.version = "2.9.3"
      ansible.inventory_path = "inventories/local/hosts"
      ansible.limit = "all"
    end
  end
end

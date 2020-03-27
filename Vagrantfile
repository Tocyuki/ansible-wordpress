# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "bento/amazonlinux-2"
  ansible_version = "2.9.3"

  config.vm.define "app" do |app|
    app.vm.network :private_network, ip: "192.168.33.10"
    app.vm.network "forwarded_port", guest: 80, host: 8080
    app.vm.provision "ansible_local" do |ansible|
      ansible.become = true
      ansible.playbook = "app.yml"
      ansible.install_mode = "pip"
      ansible.version = ansible_version
      ansible.inventory_path = "inventories/local/hosts"
      ansible.limit = "all"
    end
  end

  config.vm.define "db" do |db|
    db.vm.network :private_network, ip: "192.168.33.20"
    db.vm.provision "ansible_local" do |ansible|
      ansible.become = true
      ansible.playbook = "db.yml"
      ansible.install_mode = "pip"
      ansible.version = ansible_version
      ansible.inventory_path = "inventories/local/hosts"
      ansible.limit = "all"
    end
  end
end

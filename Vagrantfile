# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|

  # Set VM OS
  config.vm.box = "ubuntu/trusty64"
  # Forward Nginx
  config.vm.network "forwarded_port", guest: 80, host: 8000
  # Forward MySQL port to host
  config.vm.network "forwarded_port", guest: 3306, host: 3307

  # Virtualbox provider
  config.vm.provider "virtualbox" do |vb|
    vb.gui = false
    vb.memory = "1024"
    vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
  end

  # Ansible provisioner
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "ansible/all.yml"
    ansible.limit = 'all'
    ansible.inventory_path = "ansible/inventory/development/hosts"
    ansible.verbose = 'vvvv'
    ansible.vault_password_file = 'ansible/inventory/development/vaultkey'
  end

end

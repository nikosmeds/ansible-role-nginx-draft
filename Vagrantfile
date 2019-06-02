# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"

# By default, Vagrant will share your project directory to `/vagrant` inside
# the virtual machine. See https://www.vagrantup.com/docs/synced-folders/.
  config.vm.synced_folder ".", "/vagrant", disabled: true

# Configure new VM
  config.vm.network "forwarded_port", guest: 22, host: 50022
  config.vm.network "forwarded_port", guest: 80, host: 50080
  config.vm.provider  :virtualbox do |vb|
    vb.memory = 1024
    vb.cpus = 1
  end

# Configure network for nginxx-webserver
  config.vm.network "private_network", ip: "10.101.0.5"

  config.vm.provision :ansible do |ansible|
    ansible.playbook = "site.yml"
    ansible.galaxy_roles_path = "roles/requirement.yml"
  end
end

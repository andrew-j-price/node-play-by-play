# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.define :instance do |config|
    config.vm.box = "ubuntu/xenial64"
    config.vm.hostname = "node-redis-mongo"
    config.vm.network :private_network, ip: "192.168.56.156", :adapter => 2
    config.vm.provider "virtualbox" do |vb|
      vb.memory = 1024
      vb.cpus = 1
      vb.gui = false
    end
    config.vm.provision "shell", inline: $keys
    config.vm.provision "shell", inline: $deploy
    config.vm.synced_folder "app", "/home/ubuntu/app", type: "rsync"
  end
end

$keys = <<SCRIPT
  sudo cp /vagrant/authorized_keys /root/.ssh/authorized_keys
  cat /vagrant/authorized_keys >> /home/ubuntu/.ssh/authorized_keys
SCRIPT

$deploy = <<SCRIPT
  sudo apt-get install -y software-properties-common
  sudo apt-add-repository ppa:ansible/ansible
  sudo apt-get update
  sudo apt-get install -y ansible
  cd /vagrant/
  ansible-playbook deploy.yml
SCRIPT

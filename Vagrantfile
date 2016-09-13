# -*- mode: ruby -*-
# vi: set ft=ruby :
# Vagrant configuration
# https://www.vagrantup.com/docs/vagrantfile/

# settings
HOSTNAME = "docker-solo"
IP = "192.168.33.10"
DEBUG = false
HOME = Dir.home

Vagrant.configure(2) do |config|
  # Vagrant centos 7 box
  # https://atlas.hashicorp.com/centos/boxes/7
  config.vm.box = "centos/7"

  config.vm.provider "virtualbox" do |vb|
    vb.customize [
      "modifyvm", :id,
      "--name", HOSTNAME,
      "--cpus", "2",
      "--memory", "1024",
      "--vram", "64"
    ]
    vb.gui = DEBUG
  end

  config.vm.network "private_network", ip: IP
  config.vm.hostname = HOSTNAME

  # https://github.com/dotless-de/vagrant-vbguest
  config.vbguest.auto_update = false

  # comment out me after initialization
  config.ssh.username = 'root'
  config.vm.synced_folder ".", "/vagrant", :disabled => true
  config.vm.synced_folder ".", "/share"
  config.vm.synced_folder "#{HOME}/Projects/docker", "/root/projects"

  # https://www.vagrantup.com/docs/provisioning/ansible_intro.html
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "provisioning/playbook.yml"
  end
end

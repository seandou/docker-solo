# -*- mode: ruby -*-
# vi: set ft=ruby :
# Vagrant configuration
# https://www.vagrantup.com/docs/vagrantfile/

# settings
$hostname = "docker-solo"
$ip = "192.168.33.10"
$debug = false

Vagrant.configure(2) do |config|
  # Vagrant centos 7 box
  # https://atlas.hashicorp.com/centos/boxes/7
  config.vm.box = "centos/7"

  config.vm.provider "virtualbox" do |vb|
    vb.customize [
      "modifyvm", :id,
      "--name", $hostname,
      "--cpus", "2",
      "--memory", "1024",
      "--vram", "64"
    ]
    vb.gui = $debug
  end

  config.vm.network "private_network", ip: $ip
  config.vm.hostname = $hostname

  # https://github.com/dotless-de/vagrant-vbguest
  config.vbguest.auto_update = false

  config.vm.synced_folder ".", "/vagrant", :disabled => true
  config.vm.synced_folder ".", "/share"

  # https://www.vagrantup.com/docs/provisioning/ansible_intro.html
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "provisioning/playbook.yml"
  end
end

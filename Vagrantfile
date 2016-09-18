# -*- mode: ruby -*-
# vi: set ft=ruby :
# Vagrant configuration
# https://www.vagrantup.com/docs/vagrantfile/

# settings
DEBUG = false
HOME = Dir.home

Vagrant.configure(2) do |config|
  config.vm.network "private_network", type: "dhcp"

  # docker main
  config.vm.define "main" do |main|
    main.vm.box = "centos/7"

    main.vm.provider "virtualbox" do |vb|
      vb.customize [
        "modifyvm", :id,
        "--name", "docker-main",
        "--cpus", "2",
        "--memory", "1024",
        "--vram", "64"
      ]
      vb.gui = DEBUG
    end

    main.vm.network "private_network", ip: "192.168.10.10"
    main.vm.hostname = "docker-main"

    # https://www.vagrantup.com/docs/provisioning/ansible_intro.html
    main.vm.provision "ansible" do |ansible|
      ansible.playbook = "provisioning/docker-main.yml"
    end

    # https://github.com/dotless-de/vagrant-vbguest
    main.vbguest.auto_update = true
  end

  # comment out me after initialization
  # config.ssh.username = 'root'
  # config.ssh.insert_key = false
  # config.ssh.private_key_path = ["provisioning/roles/base/files/keys/id_rsa", "~/.vagrant.d/insecure_private_key"]
  # config.vm.synced_folder ".", "/vagrant", :disabled => true
  # config.vm.synced_folder ".", "/share"
  # config.vm.synced_folder "#{HOME}/Projects/docker", "/root/projects"
end

# -*- mode: ruby -*-
# vi: set ft=ruby :
# Vagrant configuration
# https://www.vagrantup.com/docs/vagrantfile/

# settings
DEBUG = false
HOME = Dir.home
CWD = Dir.pwd

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

    if File.exists? "#{CWD}/.vagrant/machines/main/virtualbox/action_provision"
      main.ssh.username = 'root'
      main.ssh.insert_key = false
      main.ssh.private_key_path = ["provisioning/roles/base/files/keys/id_rsa", "~/.vagrant.d/insecure_private_key"]
      main.vm.synced_folder ".", "/vagrant", :disabled => true
      main.vm.synced_folder ".", "/share"
      main.vm.synced_folder "#{HOME}/Projects/docker", "/root/projects"
    end
  end

  # docker node
  config.vm.define "node" do |node|
    node.vm.box = "centos/7"

    node.vm.provider "virtualbox" do |vb|
      vb.customize [
        "modifyvm", :id,
        "--name", "docker-node",
        "--cpus", "2",
        "--memory", "1024",
        "--vram", "64"
      ]
      vb.gui = DEBUG
    end

    node.vm.network "private_network", ip: "192.168.10.11"
    node.vm.hostname = "docker-node"

    node.vm.provision "ansible" do |ansible|
      ansible.playbook = "provisioning/docker-node.yml"
    end

    node.vbguest.auto_update = true

    if File.exists? "#{CWD}/.vagrant/machines/node/virtualbox/action_provision"
      node.ssh.username = 'root'
      node.ssh.insert_key = false
      node.ssh.private_key_path = ["provisioning/roles/base/files/keys/id_rsa", "~/.vagrant.d/insecure_private_key"]
      node.vm.synced_folder ".", "/vagrant", :disabled => true
      node.vm.synced_folder ".", "/share"
      node.vm.synced_folder "#{HOME}/Projects/docker", "/root/projects"
    end
  end
end

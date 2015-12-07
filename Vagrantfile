# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|

  config.vm.box = "hashicorp/precise64"

   config.vm.synced_folder "vagrantSynced", "/vagrant_data", create: true

  #define a new machine: App, the termianl machine name
  config.vm.define :App do |app_config|
    app_config.vm.box = "ubuntu"
    app_config.vm.host_name = "app"
    app_config.vm.network "private_network", ip: "192.168.33.11"
    app_config.ssh.insert_key = false

    #customize vm name, memory (this have problem if defining multiple machines), assigning same
    #name to multiple machines as prohibited in virtual box gui!!!
    #https://docs.vagrantup.com/v2/virtualbox/configuration.html
    app_config.vm.provider "virtualbox" do |v|
      v.customize ["modifyvm", :id, "--name", "app", "--memory", "512"]
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    end
  end

  #define another new machine: AnsibleSlave
  config.vm.define :AnsibleSlave do |slave_config|
  slave_config.vm.box = "hashicorp/precise64"
  slave_config.vm.host_name = "slave"
  slave_config.vm.network "private_network", ip: "192.168.33.12"
    slave_config.vm.provider "virtualbox" do |v|
      v.customize ["modifyvm", :id, "--name", "ansibleSlave", "--memory", "512"]
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    end
  end

  #define another new machine: Ansible
  config.vm.define :Ansible do |master_config|
  master_config.vm.box = "hashicorp/precise64"
  master_config.vm.host_name = "anisble"
  master_config.vm.network "private_network", ip: "192.168.33.13"

    master_config.vm.provider "virtualbox" do |v|
      v.customize ["modifyvm", :id, "--name", "ansible", "--memory", "512"]
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    end

    master_config.vm.provision "ansible" do |ansible|
      ansible.playbook = "provision/ansible/playbook.yml"
    end
  end

  config.vm.host_name = "ubuntu12-64"


end

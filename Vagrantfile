# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.
  config.vm.box = "hashicorp/precise64"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
   config.vm.synced_folder "vagrantSynced", "/vagrant_data", create: true

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  # config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
  #   vb.memory = "1024"
  # end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Define a Vagrant Push strategy for pushing to Atlas. Other push strategies
  # such as FTP and Heroku are also available. See the documentation at
  # https://docs.vagrantup.com/v2/push/atlas.html for more information.
  # config.push.define "atlas" do |push|
  #   push.app = "YOUR_ATLAS_USERNAME/YOUR_APPLICATION_NAME"
  # end

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  # config.vm.provision "shell", inline: <<-SHELL
  #   sudo apt-get update
  #   sudo apt-get install -y apache2
  # SHELL

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
  end

  config.vm.host_name = "ubuntu12-64"


end

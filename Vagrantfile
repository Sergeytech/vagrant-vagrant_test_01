# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.

#Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
#  config.vm.box = "base"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # NOTE: This will enable public access to the opened port
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine and only allow access
  # via 127.0.0.1 to disable public access
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"

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
  # config.vm.synced_folder "../data", "/vagrant_data"

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

  # Enable provisioning with a shell script. Additional provisioners such as
  # Ansible, Chef, Docker, Puppet and Salt are also available. Please see the
  # documentation for more information about their specific syntax and use.
  # config.vm.provision "shell", inline: <<-SHELL
  #   apt-get update
  #   apt-get install -y apache2
  # SHELL
#end

Vagrant.configure("2") do |config|

   config.vm.define "master" do |master|
    master.vm.box = "ubuntu/focal64"
    master.vm.hostname = "master"
    master.vm.network "public_network", ip: "192.168.1.101"
    master.vm.synced_folder "./ansible","/home/vagrant/ansible"
    #master.vm.network "forwarded_port", guest: 80, host: 8080
    #master.vm.provision "shell", path: "k8s"
    master.vm.provision "shell", inline: <<-SHELL
     sed -i 's/ChallengeResponseAuthentication no/ChallengeResponseAuthentication yes/#g' /etc/ssh/sshd_config
     service ssh restart
   SHELL
    master.vm.provider "virtualbox" do |vb|
    	vb.memory = "3072"
	    vb.cpus = "3"
	    vb.name = "master"
    end 
  end
   
    config.vm.define "host01" do |host01|
    host01.vm.box = "ubuntu/focal64"
    host01.vm.hostname = "host01"
    host01.vm.network "public_network", ip: "192.168.1.102"
    # host01.vm.synced_folder ".", "/vagrant", disabled: true
       #host01.vm.provision "shell", path: "k8s"
    host01.vm.provision "shell", inline: <<-SHELL
     sed -i 's/ChallengeResponseAuthentication no/ChallengeResponseAuthentication yes/#g' /etc/ssh/sshd_config
     service ssh restart
   SHELL
    host01.vm.provider "virtualbox" do |vb|
    	vb.memory = "2048"
	    vb.cpus = "2"
	    vb.name = "host01"
    end 
  end  

#   config.vm.define "centos" do |centos|
#   centos.vm.box = "bento/centos-7.5"
#   centos.vm.hostname = "centos"
#   centos.vm.network "public_network", ip: "192.168.1.111"
#    # centos.vm.synced_folder ".", "/vagrant", disabled: true
#      #centos.vm.provision "shell", path: "k8s"
#   centos.vm.provider "virtualbox" do |vb|
#    	vb.memory = "2048"
#	    vb.cpus = "2"
#	    vb.name = "centos"
#   end 
#end

end

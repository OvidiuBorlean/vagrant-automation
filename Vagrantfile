# -*- mode: ruby -*-
# vi: set ft=ruby :

#
Vagrant.configure("2") do |config|
  #config.vm.box = "sles-multibox.box"
  storageDisk='./diskX.vmdk'


#
 # config.vm.provider "virtualbox" do |vb|
 # vb.memory = "1024"
  config.vm.define "vm1" do |vm1|
     vm1.vm.hostname = "Machine1"
	 vm1.vm.box = "vm1"
	 vm1.vm.network "private_network", ip: '192.168.46.12', :adapter => 2
     vm1.vm.provision "shell", 
		inline: "touch /tmp/dummydfsd"
		#inline: 'cp /vagrant/vm1_keys.tar.gz /home/vagrant/.ssh/',
        #inline: 'tar xvf /home/vagrant/.ssh/vm1_keys.tar.gz -C /home/vagrant/.ssh/'

  end
  config.vm.define "vm2" do |vm2|
     vm2.vm.hostname = "Machine2"
	 vm2.vm.box = "vm2"
	 #vm2.vm.memory = "4096"
	 vm2.vm.network "private_network", ip: '192.168.46.13', :adapter => 2
     vm2.vm.provision "shell", 
		inline: "touch /tmp/dummydfsd"
		#inline: "cp /vagrant/vm2_keys.tar.gz /home/vagrant/.ssh/",
        #inline: "tar xvf /home/vagrant/.ssh/vm2_keys.tar.gz -C /home/vagrant/.ssh/"
     vm2.vm.provider "virtualbox" do |vm2hw|
	 vm2hw.memory = "4096"
	 end
	 
  end
  config.vm.define "storage" do |storage|
     storage.vm.hostname = "storage"
	 storage.vm.box = "storage"
	 storage.vm.network "private_network", ip: '192.168.46.14', :adapter => 2
     storage.vm.provision "shell", 
		inline: "touch /tmp/dummydfsd"
		#inline: "cp /vagrant/storage_keys.tar.gz /home/vagrant/.ssh/",
        #inline: "tar xvf /home/vagrant/.ssh/storage_keys.tar.gz -C /home/vagrant/.ssh/"

	 storage.vm.provider "virtualbox" do |storage|
	 
	 storage.memory = "1024"
	 
	 unless File.exist?(storageDisk)
     storage.customize [ "createhd", "--filename", storageDisk, "--format", "vmdk", "--size", 1024 * 15 ]
     end
     storage.customize ['modifyhd', storageDisk, '--type', 'writethrough']
     storage.customize [ "storageattach", :id, "--storagectl", "SATA", "--port", 1, "--device", 0, "--type", "hdd", "--medium", storageDisk ]
     
  end
  
  
  
  #end
  # config.vm.provision "shell", inline: <<-SHELL
  #   apt-get update
  #   apt-get install -y apache2
  # SHELL
  end
  end

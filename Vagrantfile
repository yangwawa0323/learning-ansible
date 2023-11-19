# -*- mode: ruby -*-
# vi: set ft=ruby :
IMAGE_NAMES = [ "generic/centos7", "hashicorp/bionic64", "generic/debian9" ]
VM_NAME = "server"
NODES = 3

Vagrant.configure("2") do |config|
    (1..NODES).each do |i|
	config.vm.define "#{VM_NAME}0#{i}" do |node|
      node.vm.box = IMAGE_NAMES[rand(IMAGE_NAMES.count)]
		node.vm.network "public_network" , ip: "192.168.0.10#{i}"
		node.vm.hostname = "#{VM_NAME}0#{i}"
		node.ssh.host = "127.0.0.1"
		# node.vm.network "forwarded_port" , guest: 80, host: "800#{i}"
		
		node.vm.provider :virtualbox do |vb|
		   vb.name = "#{VM_NAME}0#{i}"
		   vb.memory = 512
		   vb.cpus = 1
		end
		node.vm.provision "file", source: "~/.ssh/id_rsa.pub", destination: "host_ssh_public_key"
		node.vm.provision "shell", inline: <<-SHELL
			cat host_ssh_public_key >> /home/vagrant/.ssh/authorized_keys
		SHELL

	end
   end

  #config.vm.provision "ansible" do |ansible|
  #	ansible.playbook = "playbook.yml"
  #end
end

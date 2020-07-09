# -*- mode: ruby -*-
# vi: set ft=ruby :

#  If you need the VirtualBox Guest Additions, see https://github.com/dotless-de/vagrant-vbguest

Vagrant.configure("2") do |config|
	# https://app.vagrantup.com/bento/boxes/ubuntu-20.04
	config.vm.box                   = "bento/ubuntu-20.04"
	config.hostmanager.enabled 		= true
	config.hostmanager.manage_host 	= true
	config.hostmanager.manage_guest = true
	config.vm.provision "docker"
	config.vm.define "devops", primary: true do |devops|
		devops.vm.hostname = 'devops'
		devops.vm.network :private_network, ip: "192.168.99.101"
		devops.vm.provider :virtualbox do |v|
			v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
			v.customize ["modifyvm", :id, "--memory", 4000]
			v.customize ["modifyvm", :id, "--name", "devops"]
		end
		devops.vm.provision "file", source: "~/.ssh", destination: "$HOME/.ssh"
        devops.vm.provision "shell", inline: "chmod 600 /home/vagrant/.ssh/*"
		devops.vm.provision "file", source: "~/.aws", destination: "$HOME/.aws"
        devops.vm.provision "shell", inline: "chmod 600 /home/vagrant/.aws/*"
        devops.vm.provision "shell", inline: "rm -rf /home/vagrant/.aws/cli"
		devops.vm.provision "shell", inline: "apt-get install -y unzip jq tree git awscli"
		devops.vm.provision "shell", inline: "export VER='1.6.0' && wget https://releases.hashicorp.com/packer/${VER}/packer_${VER}_linux_amd64.zip && unzip packer_${VER}_linux_amd64.zip && mv packer /usr/local/bin"
	end
end
# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

def chef_common(chef)
  chef.cookbooks_path = ["cookbooks", "site-cookbooks"]
  chef.data_bags_path = "data_bags"
  chef.roles_path = "roles"
end

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  # Setup dev environment with gerrit and jenkins
  config.vm.define "devenv" do |devenv|

    devenv.vm.box = "ubuntu/trusty64"
	devenv.vm.hostname = "devenv"

	devenv.vm.provision "chef_solo" do |chef|
	  chef_common(chef)
	end

#	devenv.vm.provision "file", source: "gerrit.war", destination: "gerrit.war"
#	devenv.vm.provision "shell", path: "provision.sh"
    devenv.vm.network "forwarded_port", guest: 80, host: 8080
	devenv.vm.network "private_network", ip: "192.168.50.10"
  end

  # Setup production server

  # Setup production db
end

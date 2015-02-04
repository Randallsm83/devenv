# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

def chef_common(chef)
  chef.cookbooks_path = ["cookbooks", "site-cookbooks"]
  chef.data_bags_path = "data_bags"
  chef.roles_path = "roles"
  chef.environments_path = "environments"
end

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  # Setup workstation environment
  config.vm.define "workstation" do |workstation|

    workstation.vm.box = "ubuntu/trusty64"
	workstation.vm.hostname = "workstation"
	workstation.vm.synced_folder "~/dotfiles/", "/home/vagrant/dotfiles"

	workstation.vm.provision "chef_solo" do |chef|
	  chef_common(chef)
	end

    workstation.vm.network "forwarded_port", guest: 80, host: 8081, host_ip: "192.168.10.10"
	workstation.vm.network "private_network", ip: "192.168.10.10"
  end

  # Setup CI environment with gerrit and jenkins
  config.vm.define "ci" do |ci|

    ci.vm.box = "ubuntu/trusty64"
	ci.vm.hostname = "ci"

	ci.vm.provision "chef_solo" do |chef|
	  chef_common(chef)
	end

#	ci.vm.provision "file", source: "gerrit.war", destination: "gerrit.war"
#	ci.vm.provision "shell", path: "provision.sh"
    ci.vm.network "forwarded_port", guest: 80, host: 8082, host_ip: "192.168.10.20"
	ci.vm.network "private_network", ip: "192.168.10.20"
  end

  # Setup production server

  # Setup production db
end

# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.define "Fleet"
  config.vm.box = "ubuntu/focal64"
  # require plugin https://github.com/leighmcculloch/vagrant-docker-compose
  config.vagrant.plugins = "vagrant-docker-compose"
  # install docker and docker-compose
  config.vm.provision :docker
  config.vm.provision :docker_compose, compose_version: "1.29.2"
  # config Netwrok and shared folders
  config.vm.network "private_network", ip: "192.168.100.100"
  config.vm.network :forwarded_port, host: 1337, guest: 1337
  config.vm.synced_folder "./oqconfig", "/oqconf"
  # provision
  config.vm.provision "shell", inline: <<-SHELL
    apt-get update
    sudo apt-get install --yes nodejs npm
    sudo npm install -g n
    sudo n stable
    sudo npm install -g fleetctl
    sudo fleetctl preview
  SHELL
end

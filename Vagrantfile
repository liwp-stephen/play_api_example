# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # All Vagrant configuration is done here. The most common configuration
  # options are documented and commented below. For a complete reference,
  # please see the online documentation at vagrantup.com.

  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = "yungsang/boot2docker"
  config.vm.synced_folder ".", "/vagrant"
  config.vm.network :forwarded_port, guest: 2375, host: 2375, auto_correct: true
  config.vm.network :forwarded_port, host: 9000, guest: 9000
  config.vm.network "private_network", ip: "192.168.200.42"

  config.vm.provision "docker" do |d|
    d.pull_images "mongo"
    d.pull_images "jdauphant/play-api-example"
    d.run "mongo"
    d.run "play-api-example",
       cmd: "sbt run",
       args: "-t -p 9000:9000 -v /vagrant:/var/www/play_api_example --link mongo:mongo"
  end

  config.vm.provider "virtualbox" do |v|
    v.memory = 1280
    v.cpus = 2
  end
end

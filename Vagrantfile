# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  vm_synced_folder = "/tmp/synced_folder"
  vm_synced_port = 4000

  config.vm.box = "bento/ubuntu-18.04"
  config.vm.box_check_update = false

  # Forward default jekyll port
  config.vm.network "forwarded_port", guest: "#{vm_synced_port}", host: 8080

  config.vm.synced_folder ".", "#{vm_synced_folder}"

  config.vm.provider "virtualbox" do |vb|
    vb.gui = false
    vb.cpus = 1
    vb.memory = "512"
  end

  # Install/update dependencies
  config.vm.provision "bootstrap", type: "shell", run: "once", inline: <<-SHELL
    apt-get update -y
    apt-get install -y ruby ruby-dev make build-essential tree
    gem install jekyll bundler
  SHELL

  # Deploy jekyll site
  config.vm.provision "deploy", type: "shell", run: "never", inline: <<-SHELL
    echo "ERROR: Deployment is not configured!"
    exit 1
  SHELL

  # Run jekyll site on localhost
  config.vm.provision "serve", type: "shell", run: "never", inline: <<-SHELL
    cd #{vm_synced_folder}
    jekyll serve -I -H 0.0.0.0 -P #{vm_synced_port}
  SHELL
end

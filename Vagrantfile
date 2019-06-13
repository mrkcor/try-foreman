# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "bento/ubuntu-18.04"

  config.vm.define 'foreman' do |foreman|
    foreman.vm.hostname = 'foreman'
    foreman.vm.network "private_network", ip: "192.168.1.1"

    foreman.vm.provider :virtualbox do |vb|
      vb.customize ["modifyvm", :id, "--memory", "4096"]
    end
  end

  config.vm.define 'bandit' do |bandit|
    bandit.vm.hostname = 'bandit'
    bandit.vm.network "private_network", ip: "192.168.1.2"
  end

  config.vm.provision "shell", inline: <<-SHELL
    apt update
  SHELL
end

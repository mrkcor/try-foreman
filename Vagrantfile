# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "bento/ubuntu-18.04"

  config.vm.define 'foreman' do |foreman|
    foreman.vm.hostname = 'foreman'
    foreman.vm.network "private_network", ip: "192.168.1.2"

    foreman.vm.provider :virtualbox do |vb|
      vb.customize ["modifyvm", :id, "--memory", "4096"]
    end

    foreman.vm.provision "shell", inline: <<-SHELL
      export DEBIAN_FRONTEND=noninteractive
      hostname foreman.test

      # Update the hosts file
      cat > /etc/hosts <<EOF
127.0.0.1 localhost
192.168.1.2 foreman.test

# The following lines are desirable for IPv6 capable hosts
::1     localhost ip6-localhost ip6-loopback
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters
EOF

      # Install puppet
      apt-get -y install ca-certificates
      cd /tmp && wget https://apt.puppetlabs.com/puppet5-release-bionic.deb
      dpkg -i /tmp/puppet5-release-bionic.deb

      # Enable the Foreman repo
      echo "deb http://deb.theforeman.org/ bionic 1.20" | sudo tee /etc/apt/sources.list.d/foreman.list
      echo "deb http://deb.theforeman.org/ plugins 1.20" | sudo tee -a /etc/apt/sources.list.d/foreman.list
      wget -q https://deb.theforeman.org/pubkey.gpg -O- | sudo apt-key add -

      # Enable the Ubuntu universe repo
      add-apt-repository universe

      # Download the installer
      apt-get update && apt-get -y upgrade 
      apt-get -o Dpkg::Options::=--force-confold -o Dpkg::Options::=--force-confdef -y install foreman-installer
    SHELL
  end

  config.vm.define 'bandit' do |bandit|
    bandit.vm.hostname = 'bandit'
    bandit.vm.network "private_network", ip: "192.168.1.3"

    bandit.vm.provision "shell", inline: <<-SHELL
      export DEBIAN_FRONTEND=noninteractive
      hostname bandit.test

      # Update the hosts file
      cat > /etc/hosts <<EOF
127.0.0.1 localhost
192.168.1.3 bandit.test

# The following lines are desirable for IPv6 capable hosts
::1     localhost ip6-localhost ip6-loopback
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters
EOF
    SHELL
  end

  config.vm.provision "shell", inline: <<-SHELL
    export DEBIAN_FRONTEND=noninteractive
    apt-get update && apt-get -o Dpkg::Options::=--force-confold -o Dpkg::Options::=--force-confdef -y dist-upgrade
  SHELL
end
